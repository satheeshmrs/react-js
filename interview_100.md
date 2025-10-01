## What is React, and what are its main features?
 - React is a JavaScript library developed by Facebook for creating user interfaces, particularly in single-page applications.
 -  It enables the use of reusable components that manage their own state.
   ### Advantages
   -  component-driven architecture,
   -  optimized updates through the virtual DOM,
   -  a declarative approach for better readability,
   -  and robust community backing.

## JSX:
- JSX, short for JavaScript XML, is a syntax extension for JavaScript that allows you to write HTML-like code within JavaScript
- It makes building React components easier. JSX gets converted into JavaScript function calls,
- often by Babel. For instance, <div>Hello, world!</div> is transformed into React.createElement('div', null, 'Hello, world!').

## Babel:
 - Babel is an open-source JavaScript compiler (or transpiler).
 - Its main job is to take modern JavaScript code (using ES6+ features and beyond) and convert it into older versions of JavaScript that work on environments or browsers which don’t yet support those new features.
  ### Why Developers Use Babel
  - Browser Compatibility - Not all browsers support the latest JavaScript features (e.g., async/await, optional chaining, modules). Babel converts them into equivalent older syntax.
  - Future-Proofing - Developers can start using upcoming ECMAScript features today without waiting for all browsers to catch up.
  - Ecosystem Integration - Babel integrates seamlessly with tools like Webpack, Rollup, and Parcel to create modern build pipelines.

## Virtual DOM:
 - The virtual DOM is a simplified version of the actual DOM used by React
 - It allows for efficient UI updates by comparing the virtual DOM to the real DOM and making only the necessary changes through a process known as reconciliation.

## How Does virtual DOM in React work
 - The virtual DOM in React is an in-memory representation of the real DOM.
 - When state or props change, React creates a new virtual DOM tree, compares it to the previous one using a diffing algorithm, and efficiently updates only the parts of the real DOM that changed.

   ### Benefits:
      - It improves performance by reducing costly direct DOM manipulations and makes UI updates declarative and predictable.
   ### Downsides:
    - There's some overhead from diffing and extra memory usage, and in very dynamic UIs, it may not always outperform manual optimizations.
  
## What is difference Between React Node, React Element, and React Component
- A React Node refers to any unit that can be rendered in React, such as an element, string, number, or null.
- A React Element is an immutable object that defines what should be rendered, typically created using JSX or React.createElement.
- A React Component is either a function or class that returns React Elements, enabling the creation of reusable UI components.

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/32fc7edc-e150-4a80-9d8a-cb56ee478baa" />

## What are React Fragments used for?
- React Fragments allow you to group multiple elements without adding extra nodes to the DOM.
- They are particularly useful when you need to return multiple elements from a component but don't want to wrap them in a container element.
- You can utilize shorthand syntax <>...</> or React.Fragment.
  ```javascript
  return (
  <>
    <ChildComponent1 />
    <ChildComponent2 />
  </>
   );
    ```
## What is the purpose of the "key" prop in React?
  - In React, the key prop is used to uniquely identify elements in a list, allowing React to optimize rendering by updating and reordering items more efficiently.
  - Without unique keys, React might re-render elements unnecessarily, causing performance problems and potential bugs.

  ```javascript
  {
    items.map((item) => <ListItem key={item.id} value={item.value} />);
  }
```
## What is the consequence of using array indices as keys in React?
 - Using array indices as keys can lead to performance issues and unexpected behavior,
 - Especially when reordering or deleting items.
 - React relies on keys to identify elements uniquely, and using indices can cause components to be re-rendered unnecessarily or display incorrect data.

## What are props in React? How are they different from state?
- Props (short for properties) are inputs to React components that allow you to pass data from a parent component to a child component.
- They are immutable and are used to configure a component/They are read-only (immutable inside the child).
- Props let components be reusable and dynamic.
- In contrast, state is internal to a component and can change over time, typically due to user interactions or other events.

```javascript
  function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

function App() {
  return (
    <div>
      <Greeting name="Satheesh" />
      <Greeting name="Alex" />
    </div>
  );
}

export default App;
```
## What is the difference between React's class components and functional components?
 - Class components are ES6 classes that extend React.Component and can hold state, lifecycle methods, and other features.
 - Functional components are simpler, functional JavaScript components that take props as input and return JSX. With the introduction of hooks, functional components can now manage state and lifecycle methods, making them more versatile.
 ### Which Should You Use?
 - Use Functional Components ✅
 - Modern React (post 16.8) encourages using them.
 - Hooks provide all class features (and more).

## When should you use a class component over a function component?
 - You’re maintaining or extending an older React codebase that already uses classes.
 - You’re using very old versions of React (<16.8) where Hooks don’t exist.
 - Before React 16.8, functional components couldn’t hold state. Developers used class components with this.state.
```javascript
   class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>+1</button>
      </div>
    );
  }
}
  ```
## React Fiber
 - React Fiber is a complete rewrite of the React core algorithm,
 - designed to improve performance and enable new features like async rendering, error boundaries, and incremental rendering.
 - It breaks down the rendering process into smaller chunks, allowing React to pause, abort, or prioritize updates as needed.

## What is reconciliation?
- Reconciliation is the process by which React updates the DOM to match the virtual DOM efficiently.
- It involves comparing the new virtual DOM tree with the previous one and determining the minimum number of changes required to update the actual DOM.

  <img width="1920" height="1024" alt="image" src="https://github.com/user-attachments/assets/41491747-b908-44b0-bcd4-0917d50c5d45" />

## Shadow DOM and Virtual DOM?
- Virtual DOM → A smart copy of the page that makes updates faster by only changing what’s needed.
- Shadow DOM → A mini secret DOM inside a component that keeps its styles and structure private. ✅ Result: Encapsulation — safer, reusable components without CSS conflicts.

## What is the difference between Controlled and Uncontrolled React components?

