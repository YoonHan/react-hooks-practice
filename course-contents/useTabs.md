# useTabs(useState custom)

```javascript
import React, { useState } from "react";
import "./styles.css";

const content = [
  {
    tab: "Section 1",
    content: "Content of Section 1",
  },
  {
    tab: "Section 2",
    content: "Content of Section 2",
  },
];

const useTabs = (initialTab, allTabs) => {
  if (!allTabs || !Array.isArray(allTabs)) {
    return;
  }
  const [currentIndex, setCurrentIndex] = useState(initialTab);
  return {
    currentItem: allTabs[currentIndex],
    changeItem: setCurrentIndex,
  };
};

export const App = () => {
  const { currentItem, changeItem } = useTabs(0, content);
  return (
    <div className="App">
      {content.map((section, index) => (
        <button onClick={() => changeItem(index)}>{section.tab}</button>
      ))}
      <div>{currentItem.content}</div>
    </div>
  );
};
```

`useState`를 통해서 state를 생성하고 해당 state와 state 조작용 함수를 반환하는 새로운 `useTabs`라는 custom hook을 만들었다.
content 배열 안의 내용으로 button 을 각각 만들고, 각 버튼이 눌릴 때 state 조작 함수가 실행되도록 클릭 이벤트를 등록해주었다. 이제 버튼이 눌리면 다음과 같은 순서로 re-rendering이 일어난다.

1. `changeItem` 함수에 전달된 index 인자로 state(`currentIndex`)를 변경한다.
2. `currentIndex` state가 바뀌었으므로 `useTabs`의 return 값(currentItem)도 바뀐다.
3. 바뀐 `currentItem`에 따라 다시 렌더링을 수행한다.
