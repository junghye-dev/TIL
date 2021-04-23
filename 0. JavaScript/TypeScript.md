# TypeScript
> 출처
- [TypeScript Handbook 한글 문서](https://typescript-kr.github.io/pages/tutorials/typescript-in-5-minutes.html)
- [한눈에 보는 타입스크립트(updated)](https://heropy.blog/2020/01/27/typescript/)
- [TCP School](http://www.tcpschool.com/codingmath/notation)
- [TypeScript enum을 사용하지 않는 게 좋은 이유를 Tree-shaking 관점에서 소개합니다.](https://engineering.linecorp.com/ko/blog/typescript-enum-tree-shaking/)
- [transpile (트랜스파일) 과 compile (컴파일) 의 비교](https://ideveloper2.tistory.com/166)

JavaScript 기능들을 그대로 제공함과 동시에 TypeScript만의 타입 시스템을 구성한다.

## TypeScript를 배워야하는 이유

JavaScript
- 동적 프로그래밍 언어로서, 타입 변환이 동적으로 이루어진다.
- 쉽게 타입 변경이 가능해 유연한 개발이 가능하다.
- 사전에 특정한 타입으로 고정하지 않아, 런타임 환경에서 쉽게 에러가 난다.

TypeScript
- JavaScript에 타입 시스템을 적용하여, 컴파일 환경에서 타입 에러를 잡아낼 수 있도록 한다.

결국은 런타임 환경이 아니라, 컴파일 환경에서 내가 직접 개발을 하는 과정에서 타입 에러를 막고, 좀 더 단단한 구조의 프로그램을 만들 수 있기 위해 TypeScript를 배워야하는 것이다. (특히 프로젝트 규모가 클 때 그 필요성이 커진다.)

## 기본 타입
1. Boolean (불리언)
  
    참, 거짓
    ```typescript
    let isDone: boolean = false;
    ```
2. Number (숫자)

    부동 소수값. 16진수, 10진수, 리터럴, 2진수, 8진수 리터럴
    ```typescript
    let decimal: number = 6; // 10진수
    let hex: number = 0xf00d; // 16진수 (0부터 9까지의 숫자 및 A부터 F까지의 문자 사용)
    let binary: number = 0b1010; // 2진수 (0과 1로만 숫자로 수 표현)
    let octal: number = 0o744; // 8진수 (0부터 7까지의 숫자로 수 표현)
    ```
3. String (문자열)
    ```typescript
    let color: string = "blue";
    color = 'red';

    let fullName: string = `Bob Bobbington`;
    let age: number = 37;
    let sentence: string = `Hello, my name is ${ fullName }.I'll be ${ age + 1 } years old next month.`; // 템플릿 문자열 가능
    ```
4. Array (배열)

    두 가지 방법으로 표현 가능
    ```typescript
    // 1. 
    let list: number[] = [1, 2, 3];
    // number로 된 array

    // 2. 제네릭 배열 타입 Array<elemType>
    let list: Array<number> = [1, 2, 3];
    // array 이고, number 타입으로 이루어져있다.
    ```
5. Tuple (튜플)

    요소의 타입과 개수가 **고정**된 **배열**. 그러나 요소들의 타입이 모두 같을 필요는 없다.
    ```typescript
    // 튜플 타입으로 선언
    let x: [string, number];

    // 초기화
    x = ["hello", 10]; // 성공

    // 잘못된 초기화
    x = [10, "hello"]; // 오류(number, string 이어서)
    ```
6. Enum (열거)

    제일 헷갈리는 것.
    Enum의 각 원소는 값으로도, 타입으로도 사용될 수 있다.
    각 원소의 이름과 값은 양방향으로 매핑되어, 각자의 값만 가지고도 서로를 불러올 수 있다.
    ```typescript
    // 1. 아무것도 할당하지 않으면 배열 인덱싱처럼 0 할당 된다.
    enum Color {
      Red, // 0
      Green, // 1
      Blue // 2
    }
    let c: Color = Color.Green;
    console.log(c); // 1

    // 2. 문자열을 할당할 수도 있다.
    enum Color {
      Red = 'Red',
      Green = 'Green',
      Blue = 'Blue'
    }
    let c: Color = Color.Green;
    console.log(c); // Green
    ```
    위 typescript 코드가 js로 트랜스파일 되면
    ```typescript
    // 1. 아무것도 할당하지 않음
    var Color;

    // IIFE(즉시실행함수)
    (function (Color) {
      // 각 원소의 이름과 값이 양방향으로 매핑 된다.
      Color[Color["Red"] = 0] = "Red";
      Color[Color["Green"] = 1] = "Green";
      Color[Color["Blue"] = 2] = "Blue";
    })(Color || (Color = {}));
    
    var c = Color.Green;
    
    // 2. 문자열을 할당함
    var Color;
    
    // 일반 객체처럼 값이 할당된다
    (function (Color) {
        Color["Red"] = "Red";
        Color["Green"] = "Green";
        Color["Blue"] = "Blue";
    })(Color || (Color = {}));
    
    var c = Color.Green;
    ```
    그런데 주의할 점이 있다. enum은 typescript에만 있는 형식이라서 이를 구현하기 위해 즉시실행함수 코드를 생성하는데, 이게 Rollup과 같은 번들러에서는 '사용하지 않는 코드'라고 판단할 수 없어서 Tree-shaking이 되지 않는다고 한다.

    그래서 이 대신 **Type assertions(타입 단언)**을 이용한 **Union Types**을 사용하길 권장한다.
    ```typescript
    const Color = {
      Red: "Red",
      Green: "Green",
      Blue: "Blue"
    } as const // 타입 단언

    type Color = typeof Color[keyof typeof Color];
    
    const c: Color = Color.Green; // 'Green'

    // js 트랜스파일 후
    // 즉시실행함수가 생성되지 않는다.
    var Color = {
      Red: "Red",
      Green: "Green",
      Blue: "Blue"
    };
    var c = Color.Green;
    ```
    출처: [TypeScript enum을 사용하지 않는 게 좋은 이유를 Tree-shaking 관점에서 소개합니다.](https://engineering.linecorp.com/ko/blog/typescript-enum-tree-shaking/)
7. Any
8. Void
9. Null and Undefined
10. Never
11. Object
12. Type assertions (타입 단언)
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

- 클래스 인수에 `public`을 쓰지 않으면 이렇게 트랜스파일 된다.

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
- public 넣으면 이렇게 트랜스파일 된다.
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
