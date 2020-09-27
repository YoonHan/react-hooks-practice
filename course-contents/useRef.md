# useRef

## useRef 활용하기

- `useRef`는 component의 어느 한 부분을 선택하는 데에 사용된다. 마치 `document.getElementByID`로 요소를 선택하는 것과 같다고 보면 된다.

```javascript
import React, { useRef } from "react";
import "./styles.css";

export const App = () => {
  const input = useRef(); // reference 생성
  setTimeout(() => console.log(input.current.focus()), 3000);
  return (
    <div className="App">
      <h1>Hi</h1>
      <input ref={input} placeholder="La" />
    </div>
  );
};
```

위의 코드에서처럼 input element의 ref 속성에(React element들은 전부 ref속성을 가지고 있다) useRef로 생성한 reference를 넣어주면,
이후에는 해당 reference 객체를 통해서 ref 속성이 선언된 element에 접근할 수 있다.

위 코드는 3초뒤에 input 요소에 focus 한다.
