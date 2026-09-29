# JavaScript Language Trivia Review

## How To Use This File

This file is for interview review, not deep lesson reading.

Use each section like flashcards:

1. Read the question.
2. Answer out loud before reading the rest.
3. Compare your answer to the short explanation.
4. If you miss it, write the concept down and revisit it later.

The goal is to build fast recall for common interview trivia around language features, coercion rules, scope, and object behavior.

## Values, Types, and Coercion

### Question 1

What is the difference between `null` and `undefined`?

Short answer:

- `undefined` usually means a value is missing or has not been assigned.
- `null` usually means an empty value was assigned intentionally.

Why this matters:

- Interviewers want to know whether you understand common JavaScript value semantics instead of treating both as the same mystery value.

### Question 2

What does `typeof null` return?

Short answer:

- It returns `"object"`.

Why this matters:

- This is a famous historical quirk in JavaScript.

Common mistake:

- Saying it returns `"null"`.

### Question 3

What is the difference between primitive values and reference values?

Short answer:

- Primitive values like strings, numbers, and booleans are copied by value.
- Objects, arrays, and functions are reference values, so variables can point to the same underlying object.

Why this matters:

- This affects copying, mutation, function arguments, and React state updates.

### Question 4

What is type coercion?

Short answer:

- Type coercion is when JavaScript automatically converts one type into another during an operation.

Examples:

- `"5" + 2` becomes `"52"`
- `"5" - 2` becomes `3`

### Question 5

What is the difference between `==` and `===`?

Short answer:

- `==` allows coercion before comparison.
- `===` compares value and type without coercion.

Interview-safe guidance:

- Use `===` by default.

### Question 6

What values are falsy in JavaScript?

Short answer:

- `false`
- `0`
- `""`
- `null`
- `undefined`
- `NaN`

Why this matters:

- Conditional bugs often come from not knowing which values are falsy.

## Variables, Scope, and Hoisting

### Question 7

What is the difference between `var`, `let`, and `const`?

Short answer:

- `var` is function-scoped and hoisted in a more confusing way.
- `let` is block-scoped and can be reassigned.
- `const` is block-scoped and cannot be reassigned.

Interview-safe guidance:

- Prefer `const` by default, use `let` when reassignment is needed, avoid `var` in modern code.

### Question 8

What is hoisting?

Short answer:

- Hoisting is JavaScript's behavior of processing declarations before execution in a given scope.

Important nuance:

- Function declarations are hoisted with their definitions.
- `var` is hoisted and initialized to `undefined`.
- `let` and `const` are hoisted too, but are unavailable before initialization due to the temporal dead zone.

### Question 9

What is the temporal dead zone?

Short answer:

- It is the period between entering a scope and the line where a `let` or `const` variable is initialized.

Why this matters:

- Accessing the variable during that period throws an error.

### Question 10

What is lexical scope?

Short answer:

- Lexical scope means variable access is determined by where code is written, not where it is called from.

Why this matters:

- This is the foundation for closures.

### Question 11

What is a closure?

Short answer:

- A closure is when a function keeps access to variables from the scope where it was created, even after that outer function has finished.

Why this matters:

- Closures appear in callbacks, factories, private state patterns, and UI event handlers.

## Functions and `this`

### Question 12

What is the difference between a function declaration and a function expression?

Short answer:

- A function declaration defines a named function directly.
- A function expression creates a function as part of an expression and can be assigned to a variable.

Why this matters:

- Their hoisting behavior differs.

### Question 13

How do arrow functions differ from regular functions?

Short answer:

- Arrow functions use lexical `this`.
- They do not have their own `arguments`.
- They are often shorter for inline callbacks.

Common mistake:

- Saying arrow functions are just syntax sugar with no behavior changes.

### Question 14

What determines the value of `this` in JavaScript?

Short answer:

- `this` depends on how a function is called, except in arrow functions, which inherit `this` lexically.

Quick cases:

- method call: usually the object before the dot
- plain function call: global object or `undefined` in strict mode
- constructor call with `new`: the new instance
- arrow function: inherited from surrounding scope

### Question 15

What does `bind` do?

Short answer:

- `bind` returns a new function with a fixed `this` value and optionally fixed starting arguments.

Why this matters:

- It often comes up when passing methods as callbacks.

## Arrays, Objects, and Mutability

### Question 16

What is the difference between mutating and non-mutating array methods?

Short answer:

- Mutating methods change the original array.
- Non-mutating methods return a new array or value.

Examples:

- mutating: `push`, `pop`, `splice`, `sort`
- non-mutating: `map`, `filter`, `slice`, `concat`

### Question 17

What does the spread operator do for arrays and objects?

Short answer:

- It expands elements or properties into a new array or object.

Important nuance:

- It performs a shallow copy, not a deep copy.

### Question 18

What is object destructuring?

Short answer:

- It is a syntax for pulling properties out of an object into variables.

Example idea:

- `const { name } = user`

### Question 19

What is the difference between dot notation and bracket notation?

Short answer:

- Dot notation uses a literal property name.
- Bracket notation can use dynamic expressions or property names with special characters.

### Question 20

Why is shallow copying important to understand?

Short answer:

- Because nested objects or arrays can still be shared after a shallow copy.

Why this matters:

- This causes subtle state mutation bugs.

## Prototypes, Classes, and Inheritance

### Question 21

What is the prototype chain?

Short answer:

- It is the mechanism JavaScript uses to look up properties on objects when they are not found directly on the object itself.

### Question 22

Are JavaScript classes the same as classes in classical OOP languages?

Short answer:

- Not exactly.
- JavaScript classes are syntax built on top of prototype-based inheritance.

### Question 23

What does `new` do?

Short answer:

- It creates a new object, links it to the constructor's prototype, binds `this`, and returns the new instance unless another object is returned explicitly.

## Async and Runtime Basics

### Question 24

What is the event loop?

Short answer:

- The event loop is the runtime mechanism that coordinates synchronous execution with queued asynchronous callbacks and promise reactions.

Why this matters:

- It explains why JavaScript can handle async operations without blocking the entire program.

### Question 25

What is the difference between a promise and `async/await`?

Short answer:

- `async/await` is syntax built on top of promises.
- It makes promise-based code easier to read, but does not replace the underlying promise behavior.

### Question 26

Does `fetch` reject the promise for HTTP 404 or 500 responses?

Short answer:

- No.
- `fetch` only rejects for network-level failures.
- You still need to check `response.ok`.

## Modules and Strictness

### Question 27

What is the difference between CommonJS and ES modules?

Short answer:

- CommonJS uses `require` and `module.exports`.
- ES modules use `import` and `export`.

Why this matters:

- You will see both in Node and frontend tooling contexts.

### Question 28

What is strict mode?

Short answer:

- Strict mode enables a stricter set of JavaScript rules that helps catch mistakes and changes some legacy behaviors.

Examples:

- forbids certain silent errors
- changes some `this` behavior
- blocks accidental globals

## Fast Review Round

Use these for speed recall:

- What does `typeof null` return?
- What is the temporal dead zone?
- What does shallow copy mean?
- What is lexical scope?
- Why is `===` preferred over `==`?
- What does `new` do?
- What is the difference between promise rejection and `response.ok === false`?

## What A Good Interview Answer Sounds Like

A good trivia answer is usually:

- short
- accurate
- confident
- followed by one useful nuance

Example:

- "A closure is when a function keeps access to variables from the scope where it was created. That is why callbacks and factory functions can still use outer variables later."

That style is usually stronger than over-explaining or wandering into unrelated details.

## References

- MDN JavaScript Guide: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide
- MDN Closures: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures
- MDN Inheritance and the Prototype Chain: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
- MDN Equality comparisons and sameness: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness
