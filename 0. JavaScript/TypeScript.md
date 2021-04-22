# TypeScript
> 출처
- [TypeScript Handbook 한글 문서](https://typescript-kr.github.io/pages/tutorials/typescript-in-5-minutes.html)
- [한눈에 보는 타입스크립트(updated)](https://heropy.blog/2020/01/27/typescript/)

JavaScript 기능들을 그대로 제공함과 동시에 TypeScript만의 타입 시스템을 구성한다.

## TypeScript를 배워야하는 이유

JavaScript
- 동적 프로그래밍 언어로서, 타입 변환이 동적으로 이루어진다.
- 쉽게 타입 변경이 가능해 유연한 개발이 가능하다.
- 사전에 특정한 타입으로 고정하지 않아, 런타임 환경에서 쉽게 에러가 난다.

TypeScript
- JavaScript에 타입 시스템을 적용하여, 컴파일 환경에서 타입 에러를 잡아낼 수 있도록 한다.

결국은 런타임 환경이 아니라, 컴파일 환경에서 내가 직접 개발을 하는 과정에서 타입 에러를 막고, 좀 더 단단한 구조의 프로그램을 만들 수 있기 위해 TypeScript를 배워야하는 것이다. (특히 프로젝트 규모가 클 때 그 필요성이 커진다.)

## 타입 표기 (Type annotations)
```typescript
function greeter(person: string) {
  return 'hello' + person;
}
const person = 'Jane User';
document.body.textContent = greeter(person);
```

![image](https://user-images.githubusercontent.com/66195425/115722741-3eee9600-a3ba-11eb-976c-5e037d66b7d2.png)

- `greeter` 함수의 인자로 있는 `person` 인자의 type을 string으로 지정하자, `greeter` 함수를 사용할 때 필요한 인자 타입을 보여준다.

![image](https://user-images.githubusercontent.com/42936678/115723088-95f46b00-a3ba-11eb-8957-f3f8756e55a2.png)

- `greeter` 함수의 인자로 있는 `person` 인자값을 string이 아닌 다른 타입(여기선 number)로 지정했더니 에러 표시를 내며 string을 넣어야된다고 말해준다!

![image](https://user-images.githubusercontent.com/42936678/115723384-e4096e80-a3ba-11eb-985d-6cd4d70f9109.png)

- 이번엔 `greeter` 함수의 인자로 아무것도 안넣었더니 1개 인자가 들어와야 되는데 0개라고 에러 뿜어준다.

- 이렇게 에러가 나도, js 변환은 된다.

## 인터페이스 (Interfaces)
```typescript
// interface 표기법 주의 ( = 없음)
interface Person {
  firstName: string;
  lastName: string;
}

// interface의 타입을 따라가는 person 객체 인자
function greeter(person: Person) {
  return "Hello, " + person.firstName + " " + person.lastName;
}

// 우리가 넣고 싶은 객체
const person = {
  firstName: 'jung',
  lastName: 'lee'
}

document.body.textContent = greeter(user);
```

## 클래스 (Classes)
index.ts
  ```typescript
  class Student {
    fullName: string;
    // 생성자의 인수에 public을 사용하는 것은 그 인수의 이름으로 프로퍼티를 자동으로 생성하는 축약형이다.
    constructor(public firstName: string, public middleInitial: string, public lastName: string) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
  }

  interface Person {
    firstName: string;
    lastName: string;
  }

  function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
  }

  let user = new Student("Jane", "M.", "User");

  document.body.textContent = greeter(user);
```

- 클래스 인수에 `public`을 쓰지 않으면 이렇게 컴파일 된다.

  index.js
  ```javascript
  var Student = /** @class */ (function () {
      function Student(firstName, middleInitial, lastName) {
          this.fullName = firstName + " " + middleInitial + " " + lastName;
      }
      return Student;
  }());

  function greeter(person) {
      return "Hello, " + person.firstName + " " + person.lastName;
  }

  var user = new Student("Jane", "M.", "User");

  document.body.textContent = greeter(user);
  ```
- public 넣으면 이렇게 컴파일 된다.
  index.js
  ```javascript
  var Student = /** @class */ (function () {
      function Student(firstName, middleInitial, lastName) {
        // 이렇게 자동으로 인수와 같은 이름의 프로퍼티가 생성된다.
        this.firstName = firstName;
        this.middleInitial = middleInitial;
        this.lastName = lastName;
        this.fullName = firstName + " " + middleInitial + " " + lastName;
      }
      return Student;
  }());

  function greeter(person) {
      return "Hello, " + person.firstName + " " + person.lastName;
  
  }

  var user = new Student("Jane", "M.", "User");

  document.body.textContent = greeter(user);

  ```
