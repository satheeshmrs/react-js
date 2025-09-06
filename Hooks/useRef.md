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
In this example, the useRef hook is used to directly reference the input element, allowing us to call the focus() method on it when the button is clicked.

## Real-Life Examples of useRef
1. Accessing DOM Elements
One of the most common uses of useRef is to directly access and manipulate DOM elements. This can be particularly useful for integrating with third-party libraries or handling complex UI interactions.
```jsx
import React, { useRef, useEffect } from 'react';

function VideoPlayer() {
  const videoRef = useRef(null);

  useEffect(() => {
    // Automatically play the video when the component mounts
    videoRef.current.play();
  }, []);

  return (
    <div>
      <video ref={videoRef} width="600" controls>
        <source src="video.mp4" type="video/mp4" />
        Your browser does not support the video tag.
      </video>
    </div>
  );
}
```

In this example, the useRef hook is used to access a video element, allowing us to programmatically control the video playback.


2. Persisting Values Across Renders
Sometimes, you need to persist a value across renders without triggering a re-render. This is where useRef comes in handy.

```jsx
import React, { useState, useRef } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  const renderCount = useRef(0);

  useEffect(() => {
    renderCount.current++;
  });

  return (
    <div>
      <p>Count: {count}</p>
      <p>This component has re-rendered {renderCount.current} times</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```
Here, useRef is used to track how many times the component has re-rendered. Unlike state, updating renderCount.current does not cause the component to re-render.

3. Storing Previous State Values
You might want to compare the current state with the previous one. useRef allows you to store the previous state value without triggering a re-render.

```jsx
import React, { useState, useEffect, useRef } from 'react';

function PreviousStateExample() {
  const [name, setName] = useState('John');
  const prevNameRef = useRef('');

  useEffect(() => {
    prevNameRef.current = name;
  }, [name]);

  return (
    <div>
      <p>Current Name: {name}</p>
      <p>Previous Name: {prevNameRef.current}</p>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
    </div>
  );
}
```
In this example, useRef is used to store the previous value of the name state, allowing us to compare it with the current value.

4. Avoiding Re-Initialization of Expensive Calculations
When dealing with expensive calculations or initializations, you might want to store the result and reuse it across renders. useRef is perfect for this use case.

```jsx
import React, { useRef } from 'react';

function ExpensiveCalculationComponent() {
  const expensiveValue = useRef(calculateExpensiveValue());

  function calculateExpensiveValue() {
    console.log('Calculating expensive value...');
    return 42; // Example value
  }

  return (
    <div>
      <p>Expensive Value: {expensiveValue.current}</p>
    </div>
  );
}
```
Here, calculateExpensiveValue is only called once, during the first render. The result is stored in useRef, preventing unnecessary recalculations on subsequent renders.

5. Managing SetTimeout and SetInterval
When dealing with setTimeout or setInterval, it’s often necessary to clear these timers when the component unmounts or when the timer is no longer needed. useRef can be used to store the timer ID.

```jsx
import React, { useState, useRef, useEffect } from 'react';

function Timer() {
  const [count, setCount] = useState(0);
  const timerRef = useRef(null);

  useEffect(() => {
    timerRef.current = setInterval(() => {
      setCount((prevCount) => prevCount + 1);
    }, 1000);

    return () => {
      clearInterval(timerRef.current);
    };
  }, []);

  return <p>Count: {count}</p>;
}
```
