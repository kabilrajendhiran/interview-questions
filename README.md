### JavaScript Fundamentals

#### 1. What are the different data types in JavaScript?
JavaScript has six primitive data types:
- **String**: Represents a sequence of characters. Example: `"Hello"`
- **Number**: Represents both integer and floating-point numbers. Example: `42`, `3.14`
- **Boolean**: Represents `true` or `false`
- **Undefined**: Represents a variable that has been declared but not assigned a value
- **Null**: Represents the intentional absence of any object value
- **Symbol**: Represents a unique and immutable value (ES6)

Additionally, JavaScript has one non-primitive data type:
- **Object**: Represents a collection of properties and methods

#### 2. What is hoisting in JavaScript? Provide an example.
Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their containing scope during the compile phase. This means that you can use functions and variables before they are declared.

Example:
```javascript
console.log(myVar); // undefined
var myVar = 5;

foo(); // "Hello, world!"
function foo() {
  console.log("Hello, world!");
}
```

In the example, `myVar` and `foo` are hoisted to the top of their scope. However, only the declaration of `myVar` is hoisted, not its initialization.

#### 3. What is the difference between null and undefined?
- **Undefined**: A variable is declared but not assigned a value.
```javascript
let a;
console.log(a); // undefined
```
- **Null**: A variable is explicitly assigned to have "no value".
```javascript
let b = null;
console.log(b); // null
```

#### 4. Explain type coercion in JavaScript.
Type coercion is the process of converting a value from one type to another. JavaScript automatically converts types when necessary.
- **Implicit Coercion**: Done by JavaScript automatically.
```javascript
console.log('5' + 5); // "55" (number 5 is coerced to string)
console.log('5' - 2); // 3 (string '5' is coerced to number)
```
- **Explicit Coercion**: Done manually by the developer.
```javascript
console.log(Number('5')); // 5 (string '5' is explicitly converted to number)
```

#### 5. What is the difference between var and let? Explain hoisting with an example.
- **var**: Function-scoped or globally scoped if declared outside a function, can be re-declared and updated.
- **let**: Block-scoped, cannot be re-declared but can be updated within its scope.

Hoisting with `var`:
```javascript
console.log(a); // undefined
var a = 10;
```

Hoisting with `let`:
```javascript
console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;
```
With `let`, the variable is in a "temporal dead zone" from the start of the block until the declaration is encountered.

#### 6. What is the Temporal Dead Zone?
The Temporal Dead Zone (TDZ) is the time between entering the scope of a variable (block or function) and the point at which it is declared. During this time, the variable cannot be accessed.

Example:
```javascript
{
  console.log(c); // ReferenceError
  let c = 10;
}
```

#### 7. What is shadowing in JavaScript?
Shadowing occurs when a variable declared within a certain scope (local scope) has the same name as a variable declared in an outer scope. The inner variable "shadows" the outer variable.

Example:
```javascript
let x = 10;
function test() {
  let x = 20; // shadows the outer x
  console.log(x); // 20
}
test();
console.log(x); // 10
```

#### 8. Explain operator precedence in JavaScript.
Operator precedence determines the order in which operators are evaluated in expressions.
Example:
```javascript
let result = 3 + 4 * 2; // result is 11, because * has higher precedence than +
```
You can control precedence using parentheses:
```javascript
let result = (3 + 4) * 2; // result is 14
```

### Functions and Closures

#### 1. What are closures in JavaScript?
A closure is a function that retains access to its lexical scope, even when the function is executed outside that scope.

Example:
```javascript
function outerFunction() {
  let outerVar = 'I am outside!';
  function innerFunction() {
    console.log(outerVar); // can access outerVar
  }
  return innerFunction;
}
const myInnerFunction = outerFunction();
myInnerFunction(); // "I am outside!"
```

#### 2. What is a callback function in JavaScript?
A callback function is a function passed as an argument to another function, to be executed later.

Example:
```javascript
function greet(name, callback) {
  console.log('Hello ' + name);
  callback();
}
function sayGoodbye() {
  console.log('Goodbye!');
}
greet('Alice', sayGoodbye); // "Hello Alice", "Goodbye!"
```

#### 3. What are promises in JavaScript? What is the use of promise functions?
A promise is an object representing the eventual completion or failure of an asynchronous operation.
- **Pending**: Initial state, neither fulfilled nor rejected.
- **Fulfilled**: Operation completed successfully.
- **Rejected**: Operation failed.

Example:
```javascript
let promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Success!');
  }, 1000);
});
promise.then((message) => {
  console.log(message); // "Success!"
});
```

#### 4. What is the purpose of async and await in JavaScript? Provide examples.
`async` and `await` simplify working with promises. `async` functions return a promise, and `await` pauses the function execution until the promise resolves.

Example:
```javascript
async function fetchData() {
  let response = await fetch('https://api.example.com/data');
  let data = await response.json();
  console.log(data);
}
fetchData();
```

#### 5. What is the use of the setTimeout() function in JavaScript?
`setTimeout()` is used to execute a function after a specified delay.

Example:
```javascript
setTimeout(() => {
  console.log('This message is delayed by 2 seconds');
}, 2000);
```

#### 6. Explain the event loop, call stack, microtask queue, and callback queue.
- **Call Stack**: Stack data structure that records the function calls.
- **Event Loop**: Monitors the call stack and the callback queue, executing functions from the callback queue when the call stack is empty.
- **Microtask Queue**: Contains promises and other microtasks that are processed before the callback queue.
- **Callback Queue**: Contains callbacks from events like `setTimeout`.

### Data Structures

#### 1. What is the difference between a Map and a WeakMap?
- **Map**: Key-value pairs where keys can be any type, and it maintains the order of elements.
- **WeakMap**: Key-value pairs where keys must be objects, and it does not prevent garbage collection of keys.

### Advanced Concepts

#### 1. What are web APIs?
Web APIs are interfaces provided by the browser that allow interaction with web features (e.g., DOM manipulation, Fetch API).

#### 2. Explain scope chain and lexical environment.
- **Scope Chain**: The chain of variable environments a function has access to.
- **Lexical Environment**: The environment where variables and functions are defined.

#### 3. What is an arrow function?
An arrow function is a shorter syntax for writing functions and does not have its own `this` context.

Example:
```javascript
const add = (a, b) => a + b;
console.log(add(2, 3)); // 5
```

#### 4. What is a generator function?
A generator function can pause execution and resume at a later point. It uses the `function*` syntax and `yield` keyword.

Example:
```javascript
function* generator() {
  yield 1;
  yield 2;
  yield 3;
}
const gen = generator();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

#### 5. What is the spread operator?
The spread operator (`...`) allows an iterable to be expanded in places where multiple elements/variables are expected.

Example:
```javascript
let arr = [1, 2, 3];
let newArr = [...arr, 4, 5];
console.log(newArr); // [1, 2, 3, 4, 5]
```

#### 6. What is the use of destructuring in JavaScript?
Destructuring allows unpacking values from arrays or properties from objects into distinct variables.

Example:
```javascript
let [a, b] = [1, 2];
let {name, age} = {name: 'Alice', age: 25};
console.log(a, b); // 1, 2
console.log(name, age); // Alice, 25
```

#### 7. What is string interpolation?
String interpolation allows embedding expressions within string literals using template literals (`).

Example:
```javascript
let name = 'Alice';
let greeting = `Hello

, ${name}!`;
console.log(greeting); // "Hello, Alice!"
```

#### 8. What is the difference between for...in and for...of loops?
- **for...in**: Iterates over enumerable properties of an object.
- **for...of**: Iterates over iterable objects like arrays.

Example:
```javascript
let arr = [1, 2, 3];
for (let i in arr) {
  console.log(i); // 0, 1, 2 (indexes)
}
for (let value of arr) {
  console.log(value); // 1, 2, 3 (values)
}
```

### ReactJS Questions

#### 1. What is JSX? Provide its full form and explain.
JSX stands for JavaScript XML. It allows writing HTML elements in JavaScript and placing them in the DOM without using `createElement` or `appendChild`.

Example:
```jsx
const element = <h1>Hello, world!</h1>;
```

#### 2. What are state and props in React?
- **State**: A component's local state which can change over time and influences what gets rendered.
- **Props**: Short for properties, these are read-only inputs passed to components to configure them.

#### 3. What are hooks in ReactJS? Explain useEffect, useMemo, and useCallback.
- **useEffect**: Performs side effects in functional components.
- **useMemo**: Memoizes a value to prevent unnecessary recalculations.
- **useCallback**: Memoizes a function to prevent unnecessary re-creations.

Examples:
```jsx
useEffect(() => {
  // Side effect code
}, [dependencies]);

const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);

const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

#### 4. What is the difference between class and functional components?
- **Class Components**: Use ES6 classes, can have state and lifecycle methods.
- **Functional Components**: Use functions, can use hooks to manage state and lifecycle methods.

Example:
```jsx
class MyComponent extends React.Component {
  render() {
    return <div>Hello</div>;
  }
}

const MyComponent = () => {
  return <div>Hello</div>;
}
```

#### 5. What are ES6 new features in relation to React?
Some ES6 features commonly used in React include:
- **Arrow functions**: For concise function syntax.
- **Classes**: For class-based components.
- **Destructuring**: For extracting values from props or state.
- **Spread/Rest Operators**: For copying arrays/objects and gathering parameters.

Example:
```jsx
const { name, age } = props;
const newArr = [...oldArr, 4];
```

#### 6. What is a ref in ReactJS?
Refs provide a way to access DOM nodes or React elements directly.

Example:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }

  componentDidMount() {
    console.log(this.myRef.current); // Access DOM node
  }

  render() {
    return <div ref={this.myRef}>Hello</div>;
  }
}
```

#### 7. What is a key in ReactJS? Why is it important?
A key is a special string attribute used to identify which items have changed, are added, or are removed from a list. Keys help React optimize rendering by keeping track of elements.

Example:
```jsx
const listItems = items.map((item) =>
  <li key={item.id}>{item.text}</li>
);
```

Keys must be unique among siblings and should be stable.

### Advanced React

#### 1. What is props drilling?
Props drilling refers to the process of passing data from a top-level component to deeply nested components through multiple intermediate components. This can make the code harder to maintain and understand.

Example:
```jsx
function App() {
  const user = { name: 'Alice' };
  return <Parent user={user} />;
}

function Parent({ user }) {
  return <Child user={user} />;
}

function Child({ user }) {
  return <Grandchild user={user} />;
}

function Grandchild({ user }) {
  return <div>{user.name}</div>;
}
```

#### 2. What is a custom hook?
A custom hook is a JavaScript function that starts with "use" and can call other hooks. Custom hooks allow you to extract and reuse logic across multiple components.

Example:
```jsx
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(url)
      .then((response) => response.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      });
  }, [url]);

  return { data, loading };
}
```

#### 3. What is a Higher Order Component (HOC)?
A Higher Order Component (HOC) is a function that takes a component and returns a new component, enhancing it with additional functionality.

Example:
```jsx
function withLoading(Component) {
  return function WithLoadingComponent({ isLoading, ...props }) {
    if (isLoading) return <p>Loading...</p>;
    return <Component {...props} />;
  };
}

const ListWithLoading = withLoading(List);
```

#### 4. What is the virtual DOM? Explain the difference between virtual and real DOM.
The virtual DOM is a lightweight copy of the real DOM that React uses to optimize updates. When a component's state or props change, React updates the virtual DOM first, then compares it with the previous version (diffing). Only the differences are updated in the real DOM (reconciliation).

- **Virtual DOM**: A lightweight representation of the real DOM, used for efficient updates.
- **Real DOM**: The actual DOM tree that the browser renders and interacts with.

#### 5. Is a ReactJS app a single-page application?
A ReactJS app is typically a single-page application (SPA), meaning it loads a single HTML page and dynamically updates content without reloading the entire page. React can also be used to build multi-page applications (MPAs).

### Performance Optimization

#### 1. Explain the use of useMemo, useCallback, and memo in React.
- **useMemo**: Memoizes a computed value to avoid recalculations.
  ```jsx
  const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
  ```

- **useCallback**: Memoizes a function to avoid re-creating it on every render.
  ```jsx
  const memoizedCallback = useCallback(() => doSomething(a, b), [a, b]);
  ```

- **memo**: Higher-order component that prevents re-rendering of a component if its props have not changed.
  ```jsx
  const MemoizedComponent = React.memo(MyComponent);
  ```

### State Management

#### 1. What is Redux? Explain the flow and hooks in Redux.
Redux is a state management library for JavaScript applications. It helps manage the global state in a predictable way.

- **Flow**:
  - **Action**: An object describing what happened.
  - **Reducer**: A function that determines how the state changes in response to an action.
  - **Store**: Holds the state of the application.
  - **Dispatch**: Sends an action to the store.
  - **Selector**: Retrieves state from the store.

- **Hooks**:
  - **useSelector**: Accesses the Redux store state.
  - **useDispatch**: Dispatches actions to the Redux store.

#### 2. What is global state management?
Global state management involves managing the state of an entire application in a centralized manner, making it accessible to all components. Libraries like Redux, Context API, and MobX facilitate global state management.

#### 3. What is a slice, reducer, and action in Redux?
- **Slice**: A portion of the Redux state, managed by a specific reducer.
- **Reducer**: A function that specifies how the state changes in response to an action.
- **Action**: An object with a type property describing a state change and an optional payload.

#### 4. What are useSelector and useDispatch?
- **useSelector**: A hook to read data from the Redux store state.
  ```jsx
  const value = useSelector((state) => state.value);
  ```

- **useDispatch**: A hook to dispatch actions to the Redux store.
  ```jsx
  const dispatch = useDispatch();
  dispatch({ type: 'INCREMENT' });
  ```

### CSS and Layout

#### 1. Explain the difference between flex, media queries, and bundle in ReactJS.
- **Flex**: A CSS layout module that provides an efficient way to arrange items in a container.
  ```css
  .container {
    display: flex;
  }
  ```

- **Media Queries**: CSS techniques to apply styles based on the device's characteristics (e.g., screen size).
  ```css
  @media (max-width: 600px) {
    .container {
      flex-direction: column;
    }
  }
  ```

- **Bundle**: The process of combining multiple files into a single file for the browser, often done using tools like Webpack.

#### 2. Explain inline elements, block elements, and the different position properties (absolute, relative, fixed).
- **Inline Elements**: Do not start on a new line and only take up as much width as necessary (e.g., `<span>`, `<a>`).
- **Block Elements**: Start on a new line and take up the full width available (e.g., `<div>`, `<p>`).

- **Position Properties**:
  - **Absolute**: Positioned relative to the nearest positioned ancestor or the initial containing block if no ancestor is positioned.
    ```css
    .absolute {
      position: absolute;
      top: 10px;
      left: 10px;
    }
    ```

  - **Relative**: Positioned relative to its normal position.
    ```css
    .relative {
      position: relative;
      top: 10px;
      left: 10px;
    }
    ```

  - **Fixed**: Positioned relative to the viewport, does not move when the page is scrolled.
    ```css
    .fixed {
      position: fixed;
      top: 10px;
      left: 10px;
    }
    ```

#### 3. What are CSS selectors, pseudo-elements, and pseudo-classes?
- **CSS Selectors**: Patterns used to select the elements to style.
  ```css
  .class { ... }
  #id { ... }
  element { ... }
  ```

- **Pseudo-elements**: Used to style specific parts of an element.
  ```css
  p::first-line { ... }
  p::before { ... }
  ```

- **Pseudo-classes**: Used to define the special state of an element.
  ```css
  a:hover { ... }
  a:visited { ... }
  ```

### Additional Questions

#### 1. What is the purpose of NAND?
NAND (Not AND) is a fundamental building block in digital electronics, used in various logic circuits, including memory and processors. It performs a NOT operation after an AND operation.

#### 2. Explain pass by value and pass by reference.
- **Pass by Value**: A copy of the variable's value is passed, meaning changes to the parameter do not affect the original variable.
  ```javascript
  function modify(x) {
    x = x + 1;
  }
  let a = 1;
  modify(a);
  console.log(a); // 1
  ```

- **Pass by Reference**: A reference to the variable is passed, meaning changes to the parameter affect the original variable.
  ```javascript
  function modify(obj) {
    obj.value = obj.value + 1;
  }
  let a = { value: 1 };
  modify(a);
  console.log(a.value); // 2
  ```

#### 3. What is the difference between Array.some and Array.forEach?
- **Array.some**: Tests whether at least one element in the array passes the provided function.
  ```javascript
  const arr = [1, 2, 3];
  const hasEven = arr.some((num) => num % 2 === 0); // true
  ```

- **Array.forEach**: Executes a provided function once for each array element.
  ```javascript
  const arr = [1, 2, 3];
  arr.forEach((num) => console.log(num)); // 1, 2, 3
  ```

#### 4. Explain the reduce method in JavaScript.
The `reduce` method executes a reducer function on each element of the array, resulting in a single output value.

Example:
```javascript
const arr = [1, 2, 3, 4];
const sum = arr.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
console.log(sum); // 10
```

If you need further details or additional examples, feel free to ask!
