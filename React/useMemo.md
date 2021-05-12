# useMemo
> [velopert의 useMemo를 사용하여 연산한 값 재사용하기](https://react.vlpt.us/basic/17-useMemo.html)

Hook.
컴포넌트가 리렌더링 될 떄 재연산이 필요하지 않은 로직도 불필요하게 재실행이 되는 경우, 사용한다. **(최적화)**
- 특정 값이 바뀌었을 때만 특정 함수를 실행해서 연산을 하도록 처리
- 만약 원하는 특정 값이 바뀌지 않았으면, 컴포넌트가 리렌더링 될 때 재연산을 하는게 아니라 이전의 값을 재사용하는 것

```javascript
const count = useMemo(() => countActiveUsers(users), [users]);
// users 배열이 바뀔 때에만 countActiveUsers(users)를 실행하고, 아니면 이전의 값을 재사용한다.
```