# React Learning Roadmap

## Introduction to React
React is a JavaScript library for building user interfaces. It allows developers to create reusable UI components and manage the state of their applications efficiently. React uses a **declarative approach**, making it easier to build interactive and dynamic web applications.

---

## Table of Contents

1. [React Basics](#react-basics)
2. [JSX](#jsx)
3. [Components](#components)
4. [Props](#props)
5. [State](#state)
6. [Event Handling](#event-handling)
7. [Conditional Rendering](#conditional-rendering)
8. [Lists and Keys](#lists-and-keys)
9. [Forms](#forms)
10. [Component Lifecycle](#component-lifecycle)
11. [Hooks](#hooks)
12. [Context API](#context-api)
13. [React Router](#react-router)
14. [State Management](#state-management)
15. [Advanced Topics](#advanced-topics)
16. [Best Practices](#best-practices)
17. [Tools and Libraries](#tools-and-libraries)

---

## React Basics

### What is React?
React is a JavaScript library developed by Facebook for building user interfaces. It is **component-based**, meaning you can break down your UI into reusable pieces.

### Setting Up a React Project
You can create a React app using **Create React App**:
```bash
npx create-react-app my-app
cd my-app
npm start
```

### Folder Structure
A typical React project structure looks like this:
```
my-app/
├── public/                  # Static assets (e.g., index.html, favicon.ico)
├── src/                     # Source code
│   ├── components/          # Reusable components
│   ├── pages/               # Page components
│   ├── assets/              # Images, fonts, etc.
│   ├── styles/              # Global styles or CSS modules
│   ├── utils/               # Utility functions
│   ├── App.js               # Main application component
│   ├── index.js             # Entry point
│   └── ...                  # Other files
├── .gitignore               # Files to ignore in Git
├── package.json             # Project dependencies and scripts
├── README.md                # This file
└── ...                      # Other configuration files
```

---

## JSX

### What is JSX?
JSX (JavaScript XML) is a syntax extension for JavaScript that allows you to write HTML-like code in your React components.

### Example:
```jsx
const element = <h1>Hello, World!</h1>;
```

### Why Use JSX?
- Makes code more readable.
- Combines the power of JavaScript with HTML.

### Embedding Expressions in JSX
You can embed JavaScript expressions in JSX using curly braces `{}`.

#### Example:
```jsx
const name = "John";
const element = <h1>Hello, {name}</h1>;
```

---

## Components

### Functional Components
Functional components are JavaScript functions that return JSX.

#### Example:
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### Class Components
Class components are ES6 classes that extend `React.Component`.

#### Example:
```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### Component Composition
Components can be composed together to build complex UIs.

#### Example:
```jsx
function App() {
  return (
    <div>
      <Welcome name="John" />
      <Welcome name="Jane" />
    </div>
  );
}
```

---

## Props

### What are Props?
Props (short for properties) are used to pass data from a parent component to a child component.

#### Example:
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// Usage
<Welcome name="John" />
```

### Default Props
You can define default values for props.

#### Example:
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

Welcome.defaultProps = {
  name: "Guest",
};
```

---

## State

### What is State?
State is a built-in React object used to store data that can change over time. It is managed within a component.

#### Example (Class Component):
```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return <div>{this.state.count}</div>;
  }
}
```

#### Example (Functional Component with Hooks):
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

---

## Event Handling

### Handling Events in React
React events are named using camelCase (e.g., `onClick`).

#### Example:
```jsx
function Button() {
  function handleClick() {
    alert('Button clicked!');
  }

  return <button onClick={handleClick}>Click Me</button>;
}
```

### Passing Arguments to Event Handlers
You can pass arguments to event handlers using arrow functions.

#### Example:
```jsx
function Button({ message }) {
  return <button onClick={() => alert(message)}>Click Me</button>;
}
```

---

## Conditional Rendering

### Conditional Rendering in React
You can use JavaScript operators like `if`, `&&`, or ternary operators to conditionally render elements.

#### Example:
```jsx
function Greeting({ isLoggedIn }) {
  return isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please sign up.</h1>;
}
```

---

## Lists and Keys

### Rendering Lists
Use the `map()` function to render lists in React.

#### Example:
```jsx
function NumberList({ numbers }) {
  return (
    <ul>
      {numbers.map((number) => (
        <li key={number.toString()}>{number}</li>
      ))}
    </ul>
  );
}
```

### Keys
Keys help React identify which items have changed, been added, or been removed.

---

## Forms

### Controlled Components
In React, form elements like `<input>`, `<textarea>`, and `<select>` are controlled using state.

#### Example:
```jsx
function NameForm() {
  const [name, setName] = useState('');

  function handleSubmit(event) {
    alert('A name was submitted: ' + name);
    event.preventDefault();
  }

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## Component Lifecycle

### Lifecycle Methods (Class Components)
- `componentDidMount()`: Called after the component is rendered.
- `componentDidUpdate()`: Called after the component is updated.
- `componentWillUnmount()`: Called before the component is removed.

#### Example:
```jsx
class Timer extends React.Component {
  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({ time: new Date() });
  }

  render() {
    return <div>{this.state.time.toLocaleTimeString()}</div>;
  }
}
```

---

## Hooks

### What are Hooks?
Hooks are functions that let you use state and other React features in functional components.

### Commonly Used Hooks:
- `useState`: Manages state in functional components.
- `useEffect`: Performs side effects (e.g., fetching data).
- `useContext`: Accesses context in functional components.

#### Example:
```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [time, setTime] = useState(new Date());

  useEffect(() => {
    const timerID = setInterval(() => setTime(new Date()), 1000);
    return () => clearInterval(timerID);
  }, []);

  return <div>{time.toLocaleTimeString()}</div>;
}
```

---

## Context API

### What is Context API?
Context API provides a way to pass data through the component tree without manually passing props at every level.

#### Example:
```jsx
const ThemeContext = React.createContext('light');

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button style={{ background: theme === 'dark' ? '#333' : '#FFF' }}>Click Me</button>;
}
```

---

## React Router

### What is React Router?
React Router is a library for routing in React applications.

#### Example:
```jsx
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function App() {
  return (
    <Router>
      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </Router>
  );
}
```

---

## State Management

### What is State Management?
State management involves managing the state of your application, especially in large apps.

### Tools:
- **Redux**: A predictable state container.
- **Recoil**: A state management library for React.
- **Context API**: Built-in state management for smaller apps.

---

## Advanced Topics

### Higher-Order Components (HOCs)
HOCs are functions that take a component and return a new component with additional props or behavior.

### Render Props
Render props is a technique for sharing code between components using a prop whose value is a function.

### Error Boundaries
Error boundaries catch JavaScript errors in their child component tree and display a fallback UI.

---

## Best Practices

1. **Component Reusability**: Break down your UI into small, reusable components.
2. **State Management**: Use state management libraries like Redux or Context API for large apps.
3. **Code Splitting**: Use `React.lazy` and `Suspense` for lazy loading components.
4. **Testing**: Write unit tests using Jest and React Testing Library.

---

## Tools and Libraries

- **Create React App**: For bootstrapping React projects.
- **React DevTools**: For debugging React applications.
- **Axios**: For making HTTP requests.
- **Styled Components**: For CSS-in-JS styling.

---