# useNetwork

## useEffect, useState 활용하기

> navigator의 online property가 변화되었을 때를 감지하는 hook

```javascript
import React, { useState, useEffect } from "react";
import "./styles.css";

const useNetwork = (onChange) => {
  const [status, setStatue] = useState(navigator.onLine); // true or false
  const handleChange = () => {
    if (typeof onChange === "function") {
      onChange(navigator.onLine);
    }
    setStatue(navigator.onLine);
  };
  // componentDidMount
  useEffect(() => {
    window.addEventListener("online", handleChange);
    window.addEventListener("offline", handleChange);
    return () => {
      window.removeEventListener("online", handleChange);
      window.removeEventListener("offline", handleChange);
    };
  }, []);
  return status;
};

export const App = () => {
  const handleNetworkChange = (online) => {
    console.log(online ? "We just went online" : "We just went offline");
  };
  const online = useNetwork(handleNetworkChange);
  return (
    <div className="App">
      <h1>{online ? "Online" : "Offline"}</h1>
    </div>
  );
};
```

component가 mount되었을 때 이벤트 리스너를 등록해주고, 이후에 `navigator.online`값이 변화하면 콜백함수를 호출해 준다.
