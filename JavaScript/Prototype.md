# 프로토타입(Prototype)

> 출처: https://ko.javascript.info/prototype-inheritance
https://poiemaweb.com/js-prototype
http://insanehong.kr/post/javascript-prototype/

<br/>
객체 지향 프로그래밍에서 상속은 객체를 만들기 전에 '클래스'라고 하는 일종의 모든 
객체의 '원형'을 기반으로 새로운 객체(인스턴스)를 생성 또는 확장하는 개념이다.

자바스크립트에서는 이러한 일을 **프로토타입**을 이용해서 한다.

```javascript
const obj = {a: 1};

console.log(obj);
/*
{a: 1}
  a: 1
  __proto__:
    constructor: ƒ Object()
    hasOwnProperty: ƒ hasOwnProperty()
    isPrototypeOf: ƒ isPrototypeOf()
    propertyIsEnumerable: ƒ propertyIsEnumerable()
    toLocaleString: ƒ toLocaleString()
    toString: ƒ toString()
    valueOf: ƒ valueOf()
    __defineGetter__: ƒ __defineGetter__()
    __defineSetter__: ƒ __defineSetter__()
    __lookupGetter__: ƒ __lookupGetter__()
    __lookupSetter__: ƒ __lookupSetter__()
    get __proto__: ƒ __proto__()
    set __proto__: ƒ __proto__()
*/
```
<br/>

1. Prototype Object: Prototype Property가 가리키고 있는 것
2. Prototype Link: 자기 자신을 만들어낸 객체의 원형
3. Prototype Property: 객체 확장에 필요한 것

## 프로토타입이란?
어떠한 객체가 만들어지기 위해 그 객체의 모태가 되는 것

## 요약
(https://ko.javascript.info/prototype-inheritance#ref-1603)

- 자바스크립트의 모든 객체엔 숨김 프로퍼티 [[Prototype]]이 있는데, 이 프로퍼티는 객체나 null을 가리킵니다.
    - 여기 접근은 어떻게 하는거지?
- obj.__proto__를 사용하면 프로토타입에 접근할 수 있습니다.
    - 위에 있는 [[Prototype]]은 어떻게 접근하지
- __proto__는 [[Prototype]]의 getter·setter로 쓰이는데, 요즘엔 잘 쓰지 않습니다. 자세한 사항은 뒤쪽 챕터에서 다룰 예정입니다.
- [[Prototype]]이 참조하는 객체를 '프로토타입’이라고 합니다.
    - 그래서 '프로토타입'이다 하는 것은 '객체'인 것이다. 정말 말 그대로 원형이 되는 객체가 '프로토타입'이다.
- obj에서 프로퍼티를 읽거나 메서드를 호출하려는데 해당하는 프로퍼티나 메서드가 없으면 자바스크립트는 프로토타입에서 프로퍼티나 메서드를 찾습니다.
    - 그래서 `내가만든배열.push()` 이런게 가능한 것이다. push 메서드는 내가 만든게 아니다.
- 접근자 프로퍼티가 아닌 데이터 프로퍼티를 다루고 있다면, 쓰기나 지우기와 관련 연산은 프로토타입을 통하지 않고 객체에 직접 적용됩니다.
    - 아직 무슨 말인지 모르겠다.
- 프로토타입에서 상속받은 method라도 obj.method()를 호출하면 method 안의 this는 호출 대상 객체인 obj를 가리킵니다.
    - 아까 `내가만든배열.push()` 했을 때 push() 메서드 안의 this는 `내가만든배열`을 가리킨다.
- for..in 반복문은 객체 자체에서 정의한 프로퍼티뿐만 아니라 상속 프로퍼티도 순회 대상에 포함합니다. 반면, 키-값과 관련된 내장 메서드 대부분은 상속 프로퍼티는 제외하고 객체 자체 프로퍼티만을 대상으로 동작합니다.
    - for..in 반복문은 상속 받은 프로퍼티까지 같이 순회 해준다.

    프로토타입은 너무 어렵다....