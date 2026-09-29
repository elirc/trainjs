# Lesson 10: Framework Bridge for React-Era Development

## Goals

- Connect plain JavaScript concepts to React-style application development.
- Understand why frameworks exist without becoming dependent on magic.
- See how state, rendering, and event handling map from earlier lessons.

## Prerequisites

- Lessons 01-09.

## Concepts

React is not a replacement for JavaScript fundamentals. It is a structured way to build user interfaces with components, state, and declarative rendering.

If you understand:

- functions
- arrays and object updates
- events
- async data loading
- module structure

then you already understand a large part of what React builds on.

## Worked Example

```jsx
function TaskList({ tasks }) {
  return (
    <ul>
      {tasks.map(task => (
        <li key={task.id}>
          {task.done ? "x" : " "} {task.title}
        </li>
      ))}
    </ul>
  );
}
```

## Explaining The Code

This component is just a function that returns UI based on input data. The `map` call should feel familiar from earlier lessons. The main framework shift is that instead of manually updating the DOM node by node, you describe what the UI should look like for the current state.

## State Example

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

This is still event handling plus state updates. The framework is giving you a pattern, not replacing the underlying logic.

## Exercises

`Lab 10A`: Rewrite a plain JavaScript list-rendering pattern in React component form.

`Lab 10B`: Explain the difference between imperative DOM updates and declarative rendering.

`Lab 10C`: Describe three JavaScript fundamentals that make React easier to learn.

See the solution guide: [Lesson 10 Solutions](../../solutions/lesson-10-solutions.md)

## References

- React Learn Quick Start: https://react.dev/learn
- React Installation and gradual adoption: https://react.dev/learn/installation
- MDN JavaScript Frameworks Overview: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Frameworks_libraries

## Job-Readiness Takeaway

This lesson exists to keep you from feeling like frameworks are a separate universe. They are not. Strong JavaScript makes frameworks easier, code reviews easier, debugging easier, and interviews easier.
