# `setState()`
1. **상태**를 관리하고, 변경한다.
2. `setState()`로 인하여 상태가 변화하면 리렌더링 된다.
2. **`setState()`는 비동기로 작동한다.**<br/>한번에 여러개의 `setState()`를 사용해도 모든 변화가 완료 된 후 리렌더링 된다.
    ```javascript
    const timerAction = () => {
      const { time } = this.state;
      console.log(time);

      this.setState({
        time: time - 1;
      })
      console.log(time);
      // 이 떄의 time이 상단 setState에서 time - 1을 한 뒤, 실행이 되는 것을 보장하지 않는다.
      // setState()를 실행하고 값이 변경되기 전에 다음 라인(console.log(time))을 실행한다.
    };
    ```
3. 그래서 `setState(updater, [callback])`처럼 콜백 함수를 인자로 받으면, setState() 실행 후 -> 콜백 함수 실행 후 -> 리렌더링 된다.
4. `setState()`의 첫번째 인자인 `updater`는 함수가 될 수 있는데 아래와 같은 형태이다.
    ```javascript
    (state, props) => stateChange
    ```
    > `state`는 변경 사항이 적용되는 시점에 컴포넌트가 가지는 `state`에 대한 참조입니다.
    
    즉 여기서 첫번째 인자 `state`는 **기존에 가지고 있던 `state` 값**을 가리키며, `stateChange`는 기존의 값을 가지고 만들어 낼 **새로운 `state` 값**이 되는 것이다. (두번째 인자인 `props`도 활용 가능하다.)
    ```javascript
    this.setState((state, props) => {
      return {counter: state.counter + props.step};
      // 기존의 counter state와 props 값을 가져와서 새로운 상태를 만든다.
    });
    ```

- 출처: [setState( ) 파헤치기](https://berkbach.com/setstate-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0-28b207fc81df), [리액트 공식문서](https://ko.reactjs.org/docs/react-component.html)
