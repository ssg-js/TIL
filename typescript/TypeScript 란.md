# TypeScript 란

## 필요성

- JavaScript의 동일 연산자는 인수를 강제로 변화해, 예기치 않은 동작을 유발

```js
if ("" == 0) {
    // 참
}
```

- Javascript는 존재하는 않는 프로퍼티의 접근을 허용함

```js
const obj = {width: 10, height: 30};
const area = obj.widht * obj.ehight // NaN으로 코드가 실행됨 
```

- C, Java, Python 등은 이런 종류의 오류를 표출해주고, 일부는 컴파일 중에 오류를 알려줌. 어플리케이션 규모가 커질수록 이에 대한 관리는 비용을 발생시킴

## 정적 타입 검사자(TypeScript)

- 정적 검사 : 런타임 이전에 코드의 오류를 검출하는 것

- JavaScript의 상위 집합 언어로 JavaScript 코드의 실행을 보장함

- TypeScript 코드 검사를 하며 컴파일 후에 나온 결과는 일반 JS로 타입 정보가 존재하지 않음


