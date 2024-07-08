# 프록시(Proxy) 패턴

## 프록시 패턴

- 객체가 다른 대상 객체에 접근하기 전에, 그 **접근의 흐름을 가로채서** 해당 접근을 **필터링**하거나 **수정**하는 등의 역할을 하는 계층을 가지는 디자인 패턴
- 보통 **프록시 서버**로 이 디자인 패턴을 알고 있음

## 프록시 서버

- 메인 서버와 클라이언트 사이에 존재하는 서버

- 예시1) 메인 서버가 http를 사용할 때, 프록시 서버를 이용해 https로 바꿔 서비스 가능

- 예시2) DDoS 같은 공격적인 트래픽을 필터링하기 위한 프록시 서버(cloudflare)

## 예제 구현

```js
function createObject(target, callback) {
  const proxy = new Proxy(target, {
    set(obj, prop, value) {
      if (value !== obj[prop]) {
        const prev = obj[prop];
        obj[prop] = value;
        callback(`${prop}: [${prev}] >> [${value}] 로 변경되었음`);
      }
      return true;
    }
  });

  return proxy;
}
const a = {
  "나": "백수"
};
const b = createObject(a, console.log);
b.나 = "취업";

// 나: [백수] >> [취업] 로 변경되었음
```

#### 설명

- Proxy 객체 : 자바스크립트에서 프록시 객체를 구현해서 제공함 파라미터로 타겟 객체와 ProxyHandler라는 동작에 대한 설정값(원본 코드에는 trap이라고 표현됨)을 넘겨준다.

- ProxyHandler : 여러 가지가 있지만 set은 속성 값을 쓸 때 발동하는 trap이다.
  
  > A trap for setting a property value.
  > 
  >      * @param target The original object which is being proxied.
  > 
  >      * @param p The name or `Symbol` of the property to set.
  > 
  >      * @param receiver The object to which the assignment was originally directed.
  > 
  >      * @returns A `Boolean` indicating whether or not the property was set.
  
  (번역)
  
  > 속성 값을 설정하기 위한 트랩입니다.  
  > 
  >      * @param target 프록시 중인 원래 개체입니다.  
  > 
  >      * @param 설정할 속성의 이름 또는 'Symbol'.  
  > 
  >      * @param receiver 원래 할당이 지시된 개체입니다.  
  > 
  >      * @반품 부동산 설정 여부를 나타내는 'Boolean'을 반환합니다.

(다른 trap 참고) : [ProxyHandler 함수 - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy#handler_%ED%95%A8%EC%88%98)


