# Example-Driven JavaScript and React Training

## How To Use This Guide

This guide uses a different learning style from the main course. Instead of long concept sections followed by a few exercises, this track gives you many small code examples and then explains each one in detail.

Use it like this:

1. Read the code snippet first without reading the explanation.
2. Predict the output or behavior.
3. Say out loud what each line receives, returns, reads, or changes.
4. Read the explanation only after you have made a prediction.
5. Change one line and re-run the mental model.

This is one of the fastest ways to turn passive familiarity into real fluency.

## Section 1: Values, Variables, and References

### Example 1

```js
const a = 5;
const b = a;

console.log(a, b);
```

`a` and `b` both log `5`.

Explanation:

- `a` stores a primitive number value.
- `b = a` copies that value.
- There is no shared object here, so changing one later would not change the other.

This is the simple case. Many later bugs come from assuming objects behave the same way.

### Example 2

```js
const user = { name: "Kai" };
const sameUser = user;

sameUser.name = "Riley";

console.log(user.name);
```

This logs `"Riley"`.

Explanation:

- `user` holds a reference to an object.
- `sameUser = user` copies the reference, not a cloned object.
- Both variables point to the same underlying object.
- Mutating through one variable changes what the other sees.

If you understand this example deeply, React state updates and array/object immutability become much easier later.

### Example 3

```js
const original = { count: 1 };
const copy = { ...original };

copy.count = 2;

console.log(original.count, copy.count);
```

This logs `1 2`.

Explanation:

- The spread operator creates a new top-level object.
- `copy` and `original` are now different objects.
- Changing `copy.count` does not change `original.count`.

Important limit:

- this is a shallow copy
- nested objects are still shared unless you copy them too

### Example 4

```js
const settings = {
  theme: {
    mode: "light"
  }
};

const nextSettings = { ...settings };
nextSettings.theme.mode = "dark";

console.log(settings.theme.mode);
```

This logs `"dark"`.

Explanation:

- `nextSettings` is a new outer object.
- `theme` is still the same nested object in both places.
- That means the mutation leaks back into the original structure.

This is one of the most common beginner-to-intermediate bugs in stateful UI code.

## Section 2: Functions, Scope, and Closures

### Example 5

```js
function add(a, b) {
  return a + b;
}

console.log(add(2, 3));
```

This logs `5`.

Explanation:

- `add` receives two parameters.
- It returns a new value.
- It does not mutate outside state.

This makes the function predictable, easy to test, and easy to reuse.

### Example 6

```js
let total = 0;

function addToTotal(value) {
  total += value;
}

addToTotal(3);
addToTotal(4);

console.log(total);
```

This logs `7`.

Explanation:

- The function does not return a result.
- Instead, it changes a variable defined outside itself.
- This is a side effect.

Side effects are sometimes necessary, but they make code harder to reason about because the function's impact is not visible from the return value alone.

### Example 7

```js
function outer() {
  const topic = "closures";

  function inner() {
    return `Learning ${topic}`;
  }

  return inner();
}

console.log(outer());
```

This logs `"Learning closures"`.

Explanation:

- `inner` can access `topic` because of lexical scope.
- JavaScript resolves variable access by looking outward through the scopes where the function was defined.

This matters because nested functions are everywhere in callbacks, event handlers, and React components.

### Example 8

```js
function makeCounter() {
  let count = 0;

  return function () {
    count += 1;
    return count;
  };
}

const counter = makeCounter();

console.log(counter());
console.log(counter());
```

This logs `1` and then `2`.

Explanation:

- `makeCounter` runs once and creates a private `count` variable.
- The returned function keeps access to that variable even after `makeCounter` finishes.
- That preserved access is closure.

When this clicks, a lot of JavaScript patterns stop feeling magical.

## Section 3: Arrays and Object Transformations

### Example 9

```js
const prices = [5, 10, 15];
const doubled = prices.map(price => price * 2);

console.log(doubled);
```

This logs `[10, 20, 30]`.

Explanation:

- `map` creates a new array.
- It runs the callback once for each item.
- The callback's return value becomes the new item.

Think of `map` as "transform every item into another form."

### Example 10

```js
const users = [
  { name: "Ava", active: true },
  { name: "Noah", active: false }
];

const activeUsers = users.filter(user => user.active);
console.log(activeUsers);
```

Explanation:

- `filter` keeps items where the callback returns a truthy value.
- The original array stays unchanged.
- The result contains only matching elements.

Think of `filter` as "keep only the items that pass the rule."

### Example 11

```js
const cart = [
  { name: "Book", price: 12 },
  { name: "Pen", price: 3 }
];

const total = cart.reduce((sum, item) => sum + item.price, 0);
console.log(total);
```

This logs `15`.

Explanation:

- `reduce` combines many items into one result.
- `sum` starts at `0`.
- Each item adds its price to the running total.

Beginners often find `reduce` intimidating because two values are moving at once: the current item and the accumulated result. Slow, small examples make it easier.

### Example 12

```js
const tasks = [
  { id: 1, done: false },
  { id: 2, done: true }
];

const nextTasks = tasks.map(task =>
  task.id === 1 ? { ...task, done: true } : task
);
```

Explanation:

- This updates one item immutably.
- For the matching task, it creates a new object with a changed `done` value.
- For the other task, it keeps the original object.

This is a core React state update pattern. It appears constantly in real codebases.

## Section 4: DOM and Browser Behavior

### Example 13

```js
const button = document.querySelector("#save-btn");
button.textContent = "Save Draft";
```

Explanation:

- `querySelector` finds the first matching element.
- `textContent` changes the visible text inside the element.

The key mental model is simple: select a node, then read or update its properties.

### Example 14

```js
const form = document.querySelector("#signup-form");

form.addEventListener("submit", event => {
  event.preventDefault();
  console.log("Submitted without page refresh");
});
```

Explanation:

- The browser normally refreshes or navigates on form submission.
- `preventDefault()` stops that built-in behavior.
- Your JavaScript can then validate data or send an API request first.

This is one of the earliest patterns in interactive web apps.

### Example 15

```js
const input = document.querySelector("#search");

input.addEventListener("input", event => {
  console.log(event.target.value);
});
```

Explanation:

- The `input` event fires as the user types.
- `event.target` is the element that triggered the event.
- `value` gives the current input text.

This pattern is the bridge between user behavior and UI state.

## Section 5: Async JavaScript in Small Pieces

### Example 16

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

console.log("C");
```

This logs `A`, then `C`, then `B`.

Explanation:

- JavaScript runs synchronous code first.
- `setTimeout` schedules the callback for later.
- Even with `0`, the callback does not run immediately.

This tiny example helps explain why timing bugs happen in UI code.

### Example 17

```js
async function getMessage() {
  return "Hello";
}

getMessage().then(value => console.log(value));
```

Explanation:

- An `async` function always returns a promise.
- Even though it looks like it returns a plain string, the caller receives a promise that resolves to `"Hello"`.

That is why you can use either `await` or `.then()` when consuming it.

### Example 18

```js
async function loadUser() {
  const response = await fetch("/api/user");
  const user = await response.json();
  return user.name;
}
```

Explanation:

- The first `await` waits for the network response object.
- The second `await` waits for JSON parsing.
- Returning `user.name` resolves the outer promise with that value.

A lot of async confusion disappears when you identify each awaited step separately.

### Example 19

```js
async function loadData() {
  try {
    const response = await fetch("/api/data");

    if (!response.ok) {
      throw new Error("Request failed");
    }

    return await response.json();
  } catch (error) {
    console.error(error.message);
    return [];
  }
}
```

Explanation:

- `try/catch` handles rejected promises inside `await` code.
- `response.ok` checks HTTP success.
- Returning `[]` gives the rest of the app a safe fallback shape.

The fallback matters because downstream code often assumes it receives an array.

## Section 6: React Components and Props

### Example 20

```jsx
function Welcome() {
  return <h1>Hello, world</h1>;
}
```

Explanation:

- A React component is often just a function.
- It returns JSX, which is a syntax for describing UI.
- The UI depends on what the function returns for the current inputs.

This should feel familiar if you already understand normal JavaScript functions.

### Example 21

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

Explanation:

- `props` is an object of inputs passed into the component.
- The component renders different UI depending on those inputs.

Think of props as function arguments for UI.

### Example 22

```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}</h1>;
}
```

Explanation:

- This is object destructuring in the parameter list.
- It is equivalent to reading `props.name`, but shorter and often clearer.

This is not a React-specific trick. It is plain JavaScript syntax used inside React.

### Example 23

```jsx
function TaskList({ tasks }) {
  return (
    <ul>
      {tasks.map(task => (
        <li key={task.id}>{task.title}</li>
      ))}
    </ul>
  );
}
```

Explanation:

- The component uses `map`, just like normal JavaScript.
- Each task becomes one `<li>`.
- `key` helps React track which item is which across re-renders.

This example is a perfect reminder that React builds on JavaScript patterns you already know.

## Section 7: React State Updates

### Example 24

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

Explanation:

- `useState(0)` creates state and a setter.
- `count` is the current value for this render.
- Clicking the button schedules a state update.
- React re-renders the component with the new value.

The important detail is that UI is derived from state, not manually rewritten node by node.

### Example 25

```jsx
const [user, setUser] = useState({ name: "Avery", admin: false });

setUser({ ...user, admin: true });
```

Explanation:

- This creates a new object rather than mutating the old one.
- React state updates work best when you treat state as immutable.
- The spread keeps existing fields while updating one property.

This is the same reference-copy lesson from early JavaScript, now applied to UI state.

### Example 26

```jsx
const [items, setItems] = useState(["a", "b"]);

setItems([...items, "c"]);
```

Explanation:

- `[...]` creates a new array.
- The old items stay, and `"c"` is appended.
- This pattern is safer than mutating with `push`.

Mutation can produce confusing render behavior and harder-to-debug code.

### Example 27

```jsx
setItems(items.map(item => (item === "b" ? "B" : item)));
```

Explanation:

- This updates one item based on a rule.
- `map` returns a new array.
- Only the matching value changes.

This is one of the most common "edit one thing in a list" patterns in React.

## Section 8: Effects, Data Loading, and React Timing

### Example 28

```jsx
import { useEffect } from "react";

function Page() {
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  return <div>Page</div>;
}
```

Explanation:

- `useEffect` runs after React updates the DOM.
- The empty dependency array means this effect runs once after the initial mount.

This is often where data loading, subscriptions, or setup logic begins.

### Example 29

```jsx
useEffect(() => {
  document.title = `Count: ${count}`;
}, [count]);
```

Explanation:

- The effect depends on `count`.
- React re-runs the effect whenever `count` changes.
- This keeps the document title in sync with state.

The dependency array is not decoration. It is part of the logic contract.

### Example 30

```jsx
useEffect(() => {
  let cancelled = false;

  async function load() {
    const response = await fetch("/api/tasks");
    const data = await response.json();

    if (!cancelled) {
      setTasks(data);
    }
  }

  load();

  return () => {
    cancelled = true;
  };
}, []);
```

Explanation:

- The effect starts an async request.
- The cleanup function runs when the component unmounts.
- The `cancelled` flag prevents state updates after unmount.

This is a small example of defensive thinking around async UI behavior.

## Section 9: Conditional Rendering and UI States

### Example 31

```jsx
if (isLoading) {
  return <p>Loading...</p>;
}
```

Explanation:

- This is an early return.
- It prevents the rest of the component from rendering until loading is done.

Early returns often make components easier to read than deeply nested conditions.

### Example 32

```jsx
if (error) {
  return <p>Something went wrong: {error}</p>;
}
```

Explanation:

- This gives the error state its own explicit UI.
- Good apps do not silently fail.

When designing UI, success is only one of the states you must handle.

### Example 33

```jsx
return tasks.length === 0 ? <p>No tasks yet.</p> : <TaskList tasks={tasks} />;
```

Explanation:

- This uses a ternary expression for a compact conditional.
- If the list is empty, the user sees an empty state.
- Otherwise, the main content renders.

This is a simple but important UX pattern. Empty states are real states.

## Section 10: Reading and Debugging Small React Snippets

### Example 34

```jsx
function SearchBox() {
  const [query, setQuery] = useState("");

  return (
    <input
      value={query}
      onChange={event => setQuery(event.target.value)}
    />
  );
}
```

Explanation:

- `value={query}` makes the input controlled by React state.
- `onChange` updates that state whenever the user types.
- The visible text always reflects the current `query` value.

If the input stops updating, the first debugging questions are:

- Is `onChange` firing?
- Is state updating?
- Is `value` tied to the correct state?

### Example 35

```jsx
function SaveButton({ onSave, isSaving }) {
  return (
    <button onClick={onSave} disabled={isSaving}>
      {isSaving ? "Saving..." : "Save"}
    </button>
  );
}
```

Explanation:

- The button behavior depends entirely on props.
- `disabled={isSaving}` blocks duplicate clicks while work is in progress.
- The label also reflects the current state.

This is a nice example of "derive UI from state" instead of manually coordinating pieces separately.

### Example 36

```jsx
function Profile({ user }) {
  if (!user) {
    return null;
  }

  return <h2>{user.name}</h2>;
}
```

Explanation:

- `null` means "render nothing."
- The guard prevents trying to read `user.name` when `user` is missing.

Tiny guards like this prevent a surprising number of runtime errors.

## Section 11: Practice Prompts

Try rewriting or extending the examples above:

- Change Example 8 so the counter can decrement too.
- Change Example 12 to update a task title instead of `done`.
- Extend Example 19 so it returns an object with `data` and `error`.
- Add an error state to Example 30.
- Convert Example 35 so it also shows a success message after saving.
- Write your own example that combines `useState`, `useEffect`, and list rendering.

## Section 12: What This Training Style Is Good For

This example-driven style is especially useful when you want to get better at:

- reading code quickly
- tracing data flow
- spotting mutation bugs
- understanding React state updates
- connecting plain JavaScript patterns to framework code

If the main course teaches you the larger map, this guide helps you zoom in and build comfort with the individual steps.

## References

- MDN JavaScript Guide: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide
- MDN Closures: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures
- MDN Fetch API: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
- React Learn: https://react.dev/learn
- React State: A Component's Memory: https://react.dev/learn/state-a-components-memory
- React Synchronizing with Effects: https://react.dev/learn/synchronizing-with-effects
