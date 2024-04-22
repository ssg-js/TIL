# React의 동등 비교

## 객체 간 얇은 비교

- javascript의 Object.is 로 비교 ('=="과 '==='이 아님)

- Object.is는 ES6의 기능이기 때문에 react에서는 이를 구현한 폴리필(polyfill)을 함께 사용

- 실제 리액트에서 값을 비교할 때 사용하는 코드는 [react/packages/shared/objectIs.js at main · facebook/react · GitHub](https://github.com/facebook/react/blob/main/packages/shared/objectIs.js) 참고

```flow
// objectIs.js
function is(x: any, y: any) {
  return (
    (x === y && (x !== 0 || 1 / x === 1 / y)) || (x !== x && y !== y) // eslint-disable-line no-self-compare
  );
}

const objectIs: (x: any, y: any) => boolean =
  // $FlowFixMe[method-unbinding]
  typeof Object.is === 'function' ? Object.is : is;

export default objectIs;
// => 런타임에 Object.is 가 있으면 그대로 사용하고 없으면 대체함수 사용 
```

- 이를 기반으로 shallowEqual이라는 함수를 만들어 사용

```flow
// shallowEqual.js
import is from './objectIs';
import hasOwnProperty from './hasOwnProperty';

/**
 * Performs equality by iterating through keys on an object and returning false
 * when any key has values which are not strictly equal between the arguments.
 * Returns true when the values of all keys are strictly equal.
 */
function shallowEqual(objA: mixed, objB: mixed): boolean {
  if (is(objA, objB)) {
    return true;
  }

  if (
    typeof objA !== 'object' ||
    objA === null ||
    typeof objB !== 'object' ||
    objB === null
  ) {
    return false;
  }
  // 각 키 배열을 꺼냄 
  const keysA = Object.keys(objA);
  const keysB = Object.keys(objB);
  // 배열의 길이가 다르면 false 
  if (keysA.length !== keysB.length) {
    return false;
  }

  // Test for A's keys different from B.
  for (let i = 0; i < keysA.length; i++) {
    const currentKey = keysA[i];
    if (
      !hasOwnProperty.call(objB, currentKey) ||
      !is(objA[currentKey], objB[currentKey])
    ) {
      return false;
    }
  }

  return true;
}

export default shallowEqual;
```

- 정리하자면 Object.is로 먼저 비교를 수행한 다음, Object.is로 수행 못하는 객체 간 얇은 비교를 한 번 더 수행함

- 객체 간 얇은 배교란 객체의 첫 번째 깊이에 존재하는 값만 비교

## 얇은 비교까지 구현한 이유?

- 리액트에서 사용하는 JSX props는 객체이므로 **props는 일차적으로 비교**함

- 따라서 **props에 또 다른 객체**를 넘겨줄 시, 얇은 비교가 불가능해 **렌더링이 예상치 못하게 흘러감**

#### 예시

```tsx
import React from "react";
import { memo, useEffect, useState } from "react";

type Props = {
  counter: number
}

const Component = memo((props: Props) => {
  useEffect(() => {
    console.log('Component has been rendered!!')
  })

  return <h1>{props.counter}</h1>
})

type DeeperProps = {
  counter: {
    counter: number
  }
}
const DeeperComponent = memo((props: DeeperProps) => {
  useEffect(() => {
    console.log('DeeperComponent has been rendered!')
  })

  return <h1>{props.counter.counter}</h1>
})

export default function App() {
  const [, setCounter] = useState(0)
  function handleClick() {
    setCounter((prev) => prev + 1)
  }
  return (
    <div className="App">
      <Component counter={100} />
      <DeeperComponent counter={{ counter: 100 }} />
      <button onClick={handleClick}>+</button>
    </div>
  )
}
```

- 해당 코드에서 DeeperComponet는 얇은 비교로 불가능한 깊이(props.counter.counter)를 가짐으로 + 버튼 클릭 시 counter 값에 변화가 없어도 메모이제이션(기존에 저장된)된 컴포넌트를 반환하지 못함

![](React의%20동등%20비교_assets/2024-04-03-23-11-42-image.png)
