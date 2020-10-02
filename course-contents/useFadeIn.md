# useFadeIn

## useEffect 와 useRef 활용하기

> hooks와 animation 을 섞는 방법

```javascript
import React, { useEffect, useRef } from "react";
import "./styles.css";

const useFadeIn = (duration = 1) => {
  if (typeof duration !== "number") {
    return;
  }
  const element = useRef();
  // componentDidMount
  useEffect(() => {
    if (element.current) {
      const { current } = element;
      current.style.transition = `opacity ${duration}s`;
      current.style.opacity = 1;
    }
  }, []);
  return { ref: element, style: { opacity: 0 } };
};

export const App = () => {
  const fadeInH1 = useFadeIn(2);
  const fadeInP = useFadeIn(5);
  return (
    <div className="App">
      <h1 {...fadeInH1}>Hello</h1>
      <p {...fadeInP}>paragraph</p>
    </div>
  );
};
```

`useRef`를 활용해 React element를 참조할 reference를 만들어서 `h1`과 `p`태그에 속성으로 넣어준다.
이후에 component가 mount되면 `useEffect`의 콜백함수가 실행되면서 각 reference에 해당하는 요소에 css animation이 추가된다.
