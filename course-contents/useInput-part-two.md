# useInput Part 2

## useInput에 Validator 함수 넣기

```javascript
import React, { useState } from "react";
import "./styles.css";

const useInput = (initialValue, validator) => {
  const [value, setValue] = useState(initialValue);
  const onChange = (event) => {
    const {
      target: { value },
    } = event;
    let willUpdate = true;
    if (typeof validator === "function") {
      willUpdate = validator(value);
    }

    if (willUpdate) {
      setValue(value);
    }
  };
  return { value, onChange };
};

export const App = () => {
  const maxLen = (value) => value.length < 10;
  const name = useInput("Mr.", maxLen);
  return (
    <div className="App">
      <h1>Hello</h1>
      <input placeholder="Name" {...name} />
    </div>
  );
};
```

`useInput`에 validator인자를 추가로 받게해서 문자열의 유효성을 검증하는 로직을 더해주었다.
위의 코드에서는 useInput의 `onChange`함수는 validator로 주어진 함수의 boolean return값에 따라 input element의 값을 업데이트 할지를 결정하게 된다.
