# Introduction to useEffect

## useEffect 알아보기

- `useEffect`는 class component에서의 `componentWillUnmount`, `componentDidMount`, `componentWillUpdate` 세 가지의 life cycle에서 동작하는 hook이다.
  초기에 `componentDidMount`에 한번 실행되고, 이후에 두 번째 인자 값에 따라서 `componentWillUpdate`에서도 실행된다.

- 첫번째 인자로는 콜백 함수를 받는다. 이 콜백 함수는 두 번째 인자로 주어진 배열 안의 state값이 변하게 되면 실행된다.

- 두번째 인자는 옵션이다. 두번째 인자를 넘겨주지 않으면 모든 state 값이 변할 때 마다 첫번째 인자로 주어진 콜백 함수가 실행된다. 두번째 인자로 state 변수들의 배열을 넘겨주면 배열 안에 포함된 state들이 변할 때만 콜백 함수가 실행된다. 빈 배열을 넘겨주게 되면 어떤 state의 변화에도 콜백 함수가 실행되지 않는다.
  아래 코드에는 `number` state가 변할 때에만 콜백 함수가 실행되도록 해준 예제이다.

## Code

```javascript
import React, { useState, useEffect } from "react";
import "./styles.css";

export const App = () => {
  const sayHello = () => console.log("Hello!");
  const [number, setNumber] = useState(0);
  const [aNumber, setANumber] = useState(0);
  useEffect(() => {
    sayHello();
  }, [number]);

  return (
    <div className="App">
      <h1>Hi</h1>
      <button onClick={() => setNumber(number + 1)}>{number}</button>
      <button onClick={() => setANumber(aNumber + 1)}>{aNumber}</button>
    </div>
  );
};
```
