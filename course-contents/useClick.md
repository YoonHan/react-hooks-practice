# useClick(custom)

## useEffect, useRef 활용하기

> useRef를 활용해서 useClick custom hook을 생성한다. 이 hook은 element의 생성시에 click 이벤트를 걸지 않고, 추후에 걸어주는 역할을 한다.

이전의 `useEffect`사용법과 조금 다른 점은 `componentWillUnmount` 라이프 사이클을 활용한다는 것이다. 즉, 해당 사이클에 요소에 걸려있는 이벤트 리스너를 제거해 줄 것이다.

```javascript
import React, { useEffect, useRef } from "react";
import "./styles.css";

const useClick = (onClick) => {
  const element = useRef();

  // componentDidMount
  useEffect(() => {
    if (typeof onClick !== "function") {
      return;
    }
    // for componentDidMount, componentDidUpdate
    if (element.current) {
      element.current.addEventListener("click", onClick);
    }

    // for componentWillUmount
    return () => {
      if (element.current) {
        element.current.removeEventListener("click", onClick);
      }
    };
  }, []);
  return element;
};

export const App = () => {
  const sayHello = () => console.log("Say Hello!!");
  const title = useClick(sayHello);
  return (
    <div className="App">
      <h1 ref={title}>Hi</h1>
    </div>
  );
};
```

`useEffect`에서 빈 배열을 넣어준 것은, `componentDidMount`이후에 반복적으로 이벤트 리스너를 달아주지 않기 위함이다.
