# React and Browser Trivia Review

## How To Use This File

This file is for common interview questions about React concepts, browser APIs, rendering behavior, forms, events, and UI state vocabulary.

The goal is fast verbal recall, not writing components from scratch.

## React Fundamentals

### Question 1

What is React?

Short answer:

- React is a JavaScript library for building user interfaces from components.

Good nuance:

- It focuses on describing UI as a function of state.

### Question 2

What is JSX?

Short answer:

- JSX is a syntax that lets you write UI-like markup inside JavaScript.

Important nuance:

- It is not HTML.
- It gets transformed into JavaScript function calls.

### Question 3

What is a React component?

Short answer:

- A component is a reusable piece of UI, often written as a function that returns JSX.

### Question 4

What are props?

Short answer:

- Props are inputs passed into a component.

Why this matters:

- Props let components stay reusable and configurable.

### Question 5

What is state in React?

Short answer:

- State is data managed by a component that can change over time and trigger re-renders.

### Question 6

What causes a React component to re-render?

Short answer:

- State updates, prop changes, parent re-renders, and some context changes can all trigger re-renders.

## State and Rendering Behavior

### Question 7

Why should React state usually be treated as immutable?

Short answer:

- Immutable updates make state changes predictable and easier for React and developers to reason about.

Common mistake:

- Mutating arrays or objects directly and then expecting React to behave clearly.

### Question 8

What is the difference between controlled and uncontrolled inputs?

Short answer:

- Controlled inputs are driven by React state.
- Uncontrolled inputs rely more on the DOM's internal state.

Interview-safe guidance:

- Controlled inputs are common when the UI needs validation, live updates, or synchronized state.

### Question 9

What is conditional rendering?

Short answer:

- Conditional rendering means showing different UI based on current state or props.

### Question 10

Why do lists in React need `key` props?

Short answer:

- Keys help React identify which items changed, were added, or were removed.

Common mistake:

- Saying keys are only there to remove warnings.

### Question 11

Why is using an array index as a key sometimes a bad idea?

Short answer:

- If the list order changes, index keys can cause React to associate state with the wrong item.

## Hooks and Effects

### Question 12

What does `useState` do?

Short answer:

- `useState` adds state to a function component and gives back the current value plus a setter.

### Question 13

What does `useEffect` do?

Short answer:

- `useEffect` lets you run side effects after React renders.

Examples:

- data fetching
- subscriptions
- timers
- syncing with browser APIs

### Question 14

What is the purpose of the dependency array in `useEffect`?

Short answer:

- It tells React when the effect should re-run based on changed values.

Quick cases:

- no array: after every render
- empty array: after the first mount
- values in array: when those values change

### Question 15

What is a cleanup function in `useEffect`?

Short answer:

- It is a function returned from the effect that runs before the effect re-runs or when the component unmounts.

Why this matters:

- It is used to clean up subscriptions, timers, or other ongoing side effects.

## React Data Flow

### Question 16

What does one-way data flow mean in React?

Short answer:

- Data typically flows downward from parent components to child components through props.

### Question 17

What is “lifting state up”?

Short answer:

- It means moving shared state to the closest common parent so multiple components can use it.

### Question 18

What is prop drilling?

Short answer:

- Prop drilling is passing data through several layers of components just to reach a deeper child.

Common follow-up:

- It can sometimes be solved with better structure or context when appropriate.

## Browser and DOM Basics

### Question 19

What is the DOM?

Short answer:

- The DOM is the browser's object representation of the page structure.

### Question 20

What is event bubbling?

Short answer:

- Event bubbling is when an event starts at the target element and then propagates upward through ancestor elements.

Why this matters:

- It affects event handling behavior and event delegation patterns.

### Question 21

What does `event.preventDefault()` do?

Short answer:

- It prevents the browser's default behavior for an event.

Common example:

- stopping a form from triggering a page reload

### Question 22

What is event delegation?

Short answer:

- Event delegation is attaching one event listener to a parent and handling events from child elements through bubbling.

Why this matters:

- It can simplify dynamic UI handling.

### Question 23

What is `localStorage`?

Short answer:

- `localStorage` is a browser storage API for persisting string data across page reloads.

Important nuance:

- It stores strings, so objects usually need `JSON.stringify` and `JSON.parse`.

## Forms and Browser State

### Question 24

Why is form validation usually needed on both client and server?

Short answer:

- Client-side validation improves user experience.
- Server-side validation protects data integrity and security.

### Question 25

What is the difference between `input` and `change` events?

Short answer:

- `input` fires as the value changes during typing.
- `change` usually fires when the change is committed, depending on element type and browser behavior.

## Performance and Behavior

### Question 26

What is a re-render in React?

Short answer:

- A re-render is when React calls the component again to determine what the UI should look like for the latest state and props.

### Question 27

Does a re-render always mean the DOM is fully rebuilt?

Short answer:

- No.
- React compares what changed and updates only what is necessary.

### Question 28

Why are loading, error, and empty states important in UI interviews?

Short answer:

- They show that you think beyond the happy path and understand real user experience concerns.

## Fast Review Round

- What is JSX?
- What are props?
- What is state?
- Why do lists need keys?
- What does `useEffect` do?
- What does `preventDefault()` do?
- What is event bubbling?
- Why validate on both client and server?

## What A Good Interview Answer Sounds Like

Strong answers in this area usually:

- define the concept
- mention one practical reason it matters
- avoid drifting into implementation details unless asked

Example:

- "Controlled inputs are inputs whose value is driven by React state. They are useful when you need validation, conditional UI, or shared access to the current form value."

## References

- React Learn: https://react.dev/learn
- React State: https://react.dev/learn/state-a-components-memory
- React Conditional Rendering: https://react.dev/learn/conditional-rendering
- MDN DOM Introduction: https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction
- MDN Event bubbling: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/Event_bubbling
