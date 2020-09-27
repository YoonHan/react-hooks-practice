# useTitle(custom)

## useEffect 활용하기

> 문서의 제목을 업데이트 해주는 hook을 만들어 본다.

```javascript
import React, { useState, useEffect } from "react";
import "./styles.css";

const useTitle = (initialTitle) => {
  const [title, setTitle] = useState(initialTitle);
  // title 태그 업데이트 함수
  const updateTitle = () => {
    const htmlTitle = document.querySelector("title");
    htmlTitle.innerText = title;
  };

  // useEffect로 title state 변화 감시
  useEffect(updateTitle, [title]);
  return setTitle;
};

export const App = () => {
  const titleUpdator = useTitle("Loading...");
  setTimeout(() => titleUpdator("Home"), 5000); // 5초 뒤 title을 "Home"으로 변경
  return (
    <div className="App">
      <h1>Hi</h1>
    </div>
  );
};
```
