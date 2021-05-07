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