# Lesson 02: Control Flow, Functions, Scope, Closures, and Data Structures

## Goals

- Use conditionals and loops without losing readability.
- Understand function inputs, outputs, and side effects.
- Learn scope and closures well enough to explain them.
- Work productively with arrays and objects.

## Prerequisites

- Lesson 01 or equivalent comfort with variables and types.

## Concepts

Control flow answers the question "what should the program do next?" Functions answer the question "how should this piece of logic be packaged?" Scope answers the question "which variables are available here?" Closures answer the question "why can this function still access that variable?"

Functions become much easier to reason about when you identify three things:

- what comes in
- what comes out
- what changes outside the function

## Worked Example

```js
function calculateDiscount(price, isMember) {
  if (isMember) {
    return price * 0.9;
  }

  return price;
}

console.log(calculateDiscount(100, true));  // 90
console.log(calculateDiscount(100, false)); // 100
```

This function receives two inputs and returns one value. It does not mutate outside state, which makes it easier to test and reuse.

## Scope And Closures

```js
function makeCounter() {
  let count = 0;

  return function increment() {
    count += 1;
    return count;
  };
}

const counter = makeCounter();

console.log(counter()); // 1
console.log(counter()); // 2
```

`increment` still has access to `count` even after `makeCounter` finishes running. That preserved access is closure. Many JavaScript patterns, including event handlers and factory functions, rely on this.

## Arrays And Transformation

```js
const tasks = [
  { id: 1, done: false },
  { id: 2, done: true },
  { id: 3, done: false }
];

const incomplete = tasks.filter(task => !task.done);
console.log(incomplete);
```

`filter` returns a new array containing only matching items. It does not change the original array. Methods like `map`, `filter`, and `find` are common in production code because they express intent clearly.

## Explaining The Code

The counter example matters because it shows that functions are not just reusable code blocks. They also carry access to the environment where they were created. This is why a bug inside a callback can depend on variables that were declared much earlier.

## Exercises

`Lab 02A`: Write a function `getGrade(score)` that returns `"A"`, `"B"`, `"C"`, `"D"`, or `"F"`.

`Lab 02B`: Write a function factory called `makeGreeter(name)` that returns a function which greets that person later.

`Lab 02C`: Given an array of product objects, return a new array that contains only products currently in stock.

`Lab 02D`: Explain the difference between a function that returns a value and a function that mutates an external object.

See the solution guide: [Lesson 02 Solutions](../../solutions/lesson-02-solutions.md)

## References

- MDN Functions: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions
- MDN Closures: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures
- MDN Indexed Collections: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections

## Job-Readiness Takeaway

Real product code is mostly functions moving values around. If you can read a function signature, trace scope, and transform arrays safely, you can contribute to frontend and backend code far earlier than you might think.
