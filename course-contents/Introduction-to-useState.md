# Introduction to useState

## React Hooks의 장점

[리액트 Hooks 10분만에 사용법 배우기](https://www.youtube.com/watch?v=yS-BU6eYUDE)

- 애플리케이션 프로그래밍을 함수형(Functional)으로 바꾸어 줌. 즉, React component의 state를 관리하기 위해 Class component를 작성할 필요가 없음(불필요한 boilerplate code 가 없어짐)
- `recompose`라는 라이브러리의 아이디어가 리액트 팀에 의해 차용되어 React Hook이 됨.

## useState

```javascript
import React, { useState } from "react";
import "./styles.css";

export const App = () => {
  const [item, setItem] = useState(1);
  const incrementItem = () => setItem(item + 1);
  const decrementItem = () => setItem(item - 1);
  return (
    <div className="App">
      <h1>Hello {item}</h1>
      <h2>Start editing to see some magic happen!</h2>
      <button onClick={incrementItem}>Increment</button>
      <button onClick={decrementItem}>Decrement</button>
    </div>
  );
};
```

위의 코드에서 볼 수 있는 것처럼 component내에서 state를 관리할 때,`this.setState()`에서처럼 `this` 키워드를 사용할 필요없이 state 선언시 반환된 state 조작용 함수를 통해 state를 바로 조작할 수 있다.

## useInput(custom)

```javascript
import React, { useState } from "react";
import "./styles.css";

const useInput = (initialValue) => {
  const [value, setValue] = useState(initialValue);
  const onChange = (event) => {
    console.log(event.target);
  };
  return { value, onChange };
};

export const App = () => {
  const name = useInput("Mr.");
  return (
    <div className="App">
      <h1>Hello</h1>
      <input placeholder="Name" {...name} />
    </div>
  );
};
```

`useInput`이라는 custom hook 을 만들었다. `useState`를 사용하여 state value와 state 조작 함수를 리턴하는 hook이다. 이렇게하면 state value와 state를 조작하는 함수와 컴포넌트를 서로 다른 함수로 분리할 수 있다(재사용성 용이).
그리고 위 코드에서 주목해볼 점은 `App` functional component에서 input element의 property를 설정해줄 때, `...` spread operator를 통해 해당 element의 여러 property를 동시에 설정할 수 있다는 것이다.
