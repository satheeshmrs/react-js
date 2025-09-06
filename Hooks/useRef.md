## what it is (useRef)
The useRef hook is a powerful tool in React that often flies under the radar for many developers. While its primary purpose is to reference a DOM element, it can also be used to persist values across renders without causing a re-render. This article will explore various real-life examples of how useRef can be effectively utilized in your React projects.

## What is useRef?
The useRef hook returns a mutable object with a .current property that you can use to store a value. Unlike useState, updating a useRef value does not trigger a component re-render. Here’s a basic example:
```jsx
import React, { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```
