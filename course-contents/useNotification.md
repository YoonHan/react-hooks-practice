# useNotification

## Notification 기능 hook 으로 만들기

> Browser API인 Notification 을 사용하는 function

```javascript
import React, { useState, useEffect, useRef } from "react";
import ReactDOM from "react-dom";

const useNotification = (title, options) => {
  if (!("Notification" in window)) {
    return;
  }
  const fireNotif = () => {
    // check permission
    if (Notification.permission !== "granted") {
      Notification.requestPermission().then((permission) => {
        if (permission === "granted") {
          new Notification(title, options);
        } else {
          return;
        }
      });
    } else {
      new Notification(title, options);
    }
  };
  return fireNotif;
};

export const App = () => {
  const triggerNotif = useNotification("What is your name?", {
    body: "My name is Yoon",
  });
  return (
    <div className="App" style={{ height: "1000vh" }}>
      <h1>Hello</h1>
      <button onClick={triggerNotif}>Click Me!</button>
    </div>
  );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
