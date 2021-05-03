# 함수
> 출처: https://typescript-kr.github.io/pages/functions.html

자바스크립트와 같이 기명함수(이름이 있는)와 익명함수(이름 없는)로 만들 수 있다.

```javascript
// 기명 함수
fucntion add(x, y) {
  return x + y;
}

// 익명 함수
let myAdd = function(x, y) { return x + y };

let z = 100;

function addToZ(x, y) {
  // 함수 외부의 변수도 참조할 수 있다.
  return x + y + z;
}
```

## 함수 타입
### 함수의 타이핑

```typescript
function add(x: number, y: number): number {
  // 기명 함수
  // 파리미터 x는 number, 파라미터 y는 number
  // 함수가 반환할 값의 타입도 number (바로 옆에 써준다)
  return x + y;
}

let myAdd = function(x: number, y: number): number { return x + y };
// 익명 함수
// 기명함수와 같이 파라미터들의 타입과 리턴값의 타입을 명시해주면 된다.
```

### 함수 타입 작성하기
