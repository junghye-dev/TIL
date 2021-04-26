# 인터페이스
> 출처: https://typescript-kr.github.io/pages/interfaces.html

<br/>

1. 타입의 이름을 짓는 역할을 한다.
2. 코드 안의 계약을 정의한다. (프로젝트 외부에서 사용하는 코드 포함)

<br/><br/>

### 나의 첫 번째 인터페이스
```typescript
// printLabel 함수의 인자인 labeledObj는 객체이고, 객체안의 프로퍼티의 타입은 문자열이다.
function printLabel(labeledObj: { label: string }) {
  console.log(labeledObj.label);
}
let myObj = {size: 10, label: "Size 10 Object"};

// TypeScript는 myObj가 객체 형태인지, 이 객체안의 sting 값을 가진 label 프로퍼티가 있는지 검사한다.
printLabel(myObj); // "Size 10 Object"
```
같은 예제를 `interface`로 다시 작성해 보자.
```typescript
// 위 예제에서는 { label: string } 이렇게 타입을 정의했었다. 이번에는 interface로
!
interface LabeledValue {
  label: string;
}

function printLabel(labeledObj: LabeledValue) {
  console.log(labeledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj); // "Size 10 Object"
```
<br/><br/>
### 선택적 프로퍼티
인터페이스에 적은 모든 프로퍼티가 필요하지 않은 경우가 있다. 특정한 조건에서만 존재하거나 없을 수도 있다.

```typescript
interface SquareConfig {
  color?: string; // color 프로퍼티가 '있다면' string 타입의 값을 가진다.
  width?: number // width 프로퍼티가 '있다면' number 타입의 값을 가진다.
}

// 함수 createSquare의 인자로 config를 받고, 이 인자의 타입은 SquareConfig다.
function createSquare(config: SquareConfig): {color: string; area: number} {
  let newSquare = {color: "white", area: 100};

  // 인자로 받은 config에 color 프로퍼티가 있으면 그 값을 newSqaure에 할당해준다.
  if (config.color) {
    newSquare.color = config.color;
  }
  // 인자로 받은 config에 width 프로퍼티가 있으면 그 값의 제곱을 area에 할당해준다.
  if (config.width) {
    newSquare.area = config.width * config.width;
  }

  return newSquare;
}

let mySqaure = createSquare({color: "black"});
```
