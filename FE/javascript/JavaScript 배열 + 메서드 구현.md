# JavaScript 배열 + 메서드 구현

## 배열

- JavaScript 배열은 **크기 조정이 가능**하고 다양한 **데이터 형식을 혼합**해 저장할 수 있음 => 이 특성을 없애려면 [JavaScript 형식화 배열](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Typed_arrays)을 사용

- 배열의 요소에 접근하기 위해서는 **음수가 아닌 정수**로 접근가능 (마지막 요소는 length-1)

#### 배열 - 복사

- JavaScript 표준 내장 배열 복사 연산(전개 구문, Array.from(), Array.prototype.slice(), Array.prototype.concat())은 **얕은 복사본**을 생성함. (새로운 인스턴스를 생성하지 않기에 보통 깊은 복사보다 빠름)

- **깊은 복사**를 하고 싶은 경우 JSON.stringify()를 사용해 JSON 문자열로 변환 후, JSON.parse()로 파싱해 완전히 독립된 새 배열로 변환 가능

#### 배열 - 추가

- 마지막에 추가하는 건 push() 로 구현되어 있으므로 특정 idx에 추가하는 insert() 구현해보기

```js
Array.prototype.insert = function (idx, num) {
  let temp = this.slice(idx);

  this[idx] = num;
  for (let i = 0; i < temp.length; i++) {
    this[idx + 1 + i] = temp[i];
  }
  console.log(this);
}
```

#### 배열 - 제거

- 마지막 원소를 제거하는 건 pop() 으로 구현되어 있으므로 특정 idx를 제거하는 remove() 구현하기

```js
Array.prototype.remove = function (idx) {
  const value = this[idx];

  for (let i = idx; i < this.length; i++) {
    this[i] = this[i + 1];
  }
  this.length = this.length - 1;

  return value;
}
```
