# useBeforeLeave

## useEffect 활용하기

> 마우스 커서가 브라우저 document를 벗어낫을 때 특정 함수를 실행하게 해주는 custom hook

```javascript
import React, { useEffect } from "react";
import "./styles.css";

const useBeforeLeave = (onBefore) => {
  if (typeof onBefore !== "function") {
    return;
  }
  const handler = (event) => {
    const { clientY } = event;
    if (clientY <= 0) {
      onBefore();
    }
  };
  useEffect(() => {
    document.addEventListener("mouseleave", handler);
    return () => document.removeEventListener("mouseleave", handler);
  }, []);
};

export const App = () => {
  const begForLife = () => console.log("Please don't leave!");
  useBeforeLeave(begForLife);
  return (
    <div className="App">
      <h1>Hello</h1>
    </div>
  );
};
```
