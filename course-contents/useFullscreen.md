# useFullScreen

## useRef 활용하기

> 특정 요소를 전체화면으로 만들어주는 hook

```javascript
import React, { useRef } from "react";
import "./styles.css";

const useFullscreen = () => {
  const element = useRef();
  const triggerFullscreen = () => {
    if (element.current) {
      element.current.requestFullscreen();
    }
  };
  const exitFullscreen = () => {
    document.exitFullscreen();
  };
  return { element, triggerFullscreen, exitFullscreen };
};

export const App = () => {
  const { element, triggerFullscreen, exitFullscreen } = useFullscreen();
  return (
    <div>
      <div ref={element}>
        <img ref={element} src="https://picsum.photos/200" alt="dummy" />
        <button onClick={exitFullscreen}>Exit fullscreen</button>
      </div>
      <button onClick={triggerFullscreen}>Make fullscreen</button>
    </div>
  );
};
```

`requestFullscreen`, `exitFullscreen`은 react에서 자체적으로 제공하는 함수이다.
