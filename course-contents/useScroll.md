# useScroll

## useState, useEffect 활용하기

> scroll을 할 때 y값에 따라 요소의 css style을 변화시키는 hook

```javascript
import React, { useEffect, useState } from "react";
import "./styles.css";

const useScroll = () => {
  const [state, setState] = useState({
    x: 0,
    y: 0,
  });
  const onScroll = () => {
    setState({ x: window.scrollX, y: window.scrollY });
  };
  useEffect(() => {
    window.addEventListener("scroll", onScroll);
    return () => {
      window.removeEventListener("scroll", onScroll);
    };
  }, []);
  return state;
};

export const App = () => {
  const { y } = useScroll();
  return (
    <div className="App" style={{ height: "1000vh" }}>
      <h1 style={{ position: "fixed", color: y > 100 ? "red" : "blue" }}>
        Hello
      </h1>
    </div>
  );
};
```

scroll 의 y좌표 값을 state로 관리하면서, scroll 이벤트가 발생할 때 마다 y좌표 값을 업데이트 해준다.
그러면 y좌표가 100보다 커지는 순간 `h1`요소의 스타일이 바뀌게 된다.
