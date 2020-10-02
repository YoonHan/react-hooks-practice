# useConfirm & usePreventLeave

## 함수형 프로그래밍 맛보기

### useConfirm

```javascript
import React from "react";
import "./styles.css";

const useConfirm = (message = "", onConfirm, onCancel) => {
  if (!onConfirm || typeof onConfirm !== "function") {
    return;
  }
  if (!onCancel || typeof onCancel !== "function") {
    return;
  }
  const confirmAction = () => {
    if (confirm(message)) {
      onConfirm();
    } else {
      onCancel();
    }
  };
  return confirmAction;
};

export const App = () => {
  const deleteWorld = () => console.log("Deleting World..");
  const abort = () => console.log("Aborted");
  const confirmDelete = useConfirm("Are u sure?", deleteWorld, abort);
  return (
    <div className="App">
      <h1>Hi</h1>
      <button onClick={confirmDelete}>Delete the World</button>
    </div>
  );
};
```

`useEffect`나 `useState`를 쓰지 않았기 때문에 엄밀히 말하면 hook은 아니다. 하지만 함수형 프로그래밍을 이해하는데에 좋은 예제라서 만들어 보았다.

`useConfirm`은 callback함수와 rejection 함수를 받아서 confirmAction 함수를 돌려주는 함수이다. return된 confirmAction함수는 `useConfirm`에 전달된 callback과 rejection 인자를 closure로 가지고 있어서 추후에 해당 함수들을 호출할 수 있다.

### usePreventLeave

> 사용자가 현재 창을 닫거나 새로고침을 할 때, 페이지를 떠나겠냐는 알람 창을 띄워준다.

```javascript
import React from "react";
import "./styles.css";

const usePreventLeave = () => {
  const listener = (event) => {
    event.preventDefault();
    event.returnValue = "";
  };
  const enablePrevent = () => window.addEventListener("beforeunload", listener);
  const disablePrevent = () =>
    window.removeEventListener("beforeunload", listener);

  return { enablePrevent, disablePrevent };
};

export const App = () => {
  const { enablePrevent, disablePrevent } = usePreventLeave();
  return (
    <div className="App">
      <button onClick={enablePrevent}>Protect</button>
      <button onClick={disablePrevent}>Unprotect</button>
    </div>
  );
};
```
