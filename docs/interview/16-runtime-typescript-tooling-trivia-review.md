# Runtime, TypeScript, and Tooling Trivia Review

## How To Use This File

This file covers the “other questions” that often appear around JavaScript interviews:

- async behavior
- runtime terminology
- modules
- Node basics
- TypeScript basics
- testing and tooling vocabulary

These are often asked as short verbal questions to check whether you can operate inside a modern JavaScript codebase.

## Async and Runtime Concepts

### Question 1

What is a promise?

Short answer:

- A promise is an object representing the eventual completion or failure of an asynchronous operation.

### Question 2

What are the main promise states?

Short answer:

- pending
- fulfilled
- rejected

### Question 3

What does `async` mean on a function?

Short answer:

- It means the function always returns a promise.

### Question 4

What does `await` do?

Short answer:

- It pauses execution inside an async function until a promise settles, then gives the resolved value or throws the rejection.

Important nuance:

- It does not pause the whole program.

### Question 5

What is the event loop used for?

Short answer:

- It coordinates execution of synchronous code with queued async callbacks and promise reactions.

### Question 6

What is the difference between synchronous and asynchronous code?

Short answer:

- Synchronous code runs in sequence and blocks the current flow until it finishes.
- Asynchronous code allows the program to continue while waiting for later work.

## APIs, Networking, and JSON

### Question 7

What does `JSON.stringify` do?

Short answer:

- It converts a JavaScript value into a JSON string.

### Question 8

What does `JSON.parse` do?

Short answer:

- It converts a JSON string into a JavaScript value.

### Question 9

What is an HTTP status code?

Short answer:

- It is a numeric code in an HTTP response that indicates the general result of the request.

Examples:

- `200` success
- `201` created
- `400` bad request
- `404` not found
- `500` server error

### Question 10

What does `response.ok` mean in `fetch`?

Short answer:

- It indicates whether the HTTP status is in the successful range.

### Question 11

What is the difference between authentication and authorization?

Short answer:

- Authentication checks who you are.
- Authorization checks what you are allowed to do.

## Node.js and Modules

### Question 12

What is Node.js?

Short answer:

- Node.js is a JavaScript runtime that lets JavaScript run outside the browser.

### Question 13

What is `package.json` used for?

Short answer:

- It stores project metadata, dependencies, and scripts.

### Question 14

What is the difference between dependencies and devDependencies?

Short answer:

- Dependencies are needed for the application to run.
- devDependencies are mainly used for development tools like testing, linting, or building.

### Question 15

What are npm scripts?

Short answer:

- They are named commands defined in `package.json` to standardize project tasks.

### Question 16

What is the difference between CommonJS and ES modules?

Short answer:

- CommonJS uses `require` and `module.exports`.
- ES modules use `import` and `export`.

## TypeScript Basics

### Question 17

What is TypeScript?

Short answer:

- TypeScript is JavaScript plus static typing and extra tooling support.

### Question 18

Why do teams use TypeScript?

Short answer:

- It helps catch mistakes earlier, improves editor support, and makes code contracts clearer in larger codebases.

### Question 19

What is a type annotation?

Short answer:

- A type annotation explicitly states the expected type of a variable, parameter, or return value.

### Question 20

What is the difference between a `type` alias and an `interface`?

Short answer:

- Both can describe object shapes.
- Interfaces are often used for object-oriented or extendable object contracts.
- Type aliases are more flexible for unions and other combinations.

Interview-safe guidance:

- In many beginner-to-intermediate cases, either can work.

### Question 21

What is a union type?

Short answer:

- A union type allows a value to be one of several possible types.

Example idea:

- `string | null`

### Question 22

What does TypeScript not do?

Short answer:

- It does not automatically make logic correct.
- It does not replace runtime validation.
- It does not remove the need to understand JavaScript.

## Testing and Quality Vocabulary

### Question 23

What is a unit test?

Short answer:

- A unit test checks a small isolated piece of behavior, often a single function or narrow module behavior.

### Question 24

What is the difference between unit tests and integration tests?

Short answer:

- Unit tests focus on isolated behavior.
- Integration tests check how multiple parts work together.

### Question 25

Why are pure functions easier to test?

Short answer:

- They depend only on their inputs and return outputs without hidden side effects.

### Question 26

What is a mock?

Short answer:

- A mock is a test double used to replace or simulate part of a system during testing.

### Question 27

What is linting?

Short answer:

- Linting is automated static checking for code style issues, mistakes, and risky patterns.

### Question 28

What is formatting?

Short answer:

- Formatting automatically normalizes the appearance of code, such as spacing and line breaks.

### Question 29

What is transpilation?

Short answer:

- Transpilation converts source code from one version or form into another, such as modern JavaScript or TypeScript into code a target environment can run.

## Practical Interview Questions

### Question 30

Why is server-side validation still required even if the frontend validates input?

Short answer:

- Client-side validation can be bypassed.
- The server must still protect data and business rules.

### Question 31

Why is TypeScript not a replacement for tests?

Short answer:

- TypeScript checks type-level assumptions, but tests verify behavior and logic.

### Question 32

Why is understanding promises still important if you use `async/await`?

Short answer:

- Because `async/await` is built on promises, and many APIs, errors, and concurrency patterns still depend on understanding them directly.

## Fast Review Round

- What does `async` do to a function?
- What does `await` not do?
- What is the difference between authn and authz?
- What belongs in `package.json`?
- Why use TypeScript?
- Why are pure functions easier to test?
- What is transpilation?

## What A Good Interview Answer Sounds Like

A strong answer here is usually:

- one sentence definition
- one sentence on why it matters in a real project

Example:

- "TypeScript is JavaScript with static typing and stronger tooling. Teams use it to catch mismatched assumptions earlier and make larger codebases easier to navigate."

That is usually enough unless the interviewer asks for more detail.

## References

- Node.js Learn: https://nodejs.org/en/learn
- MDN Using Promises: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises
- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro
- Jest Docs: https://jestjs.io/help
- MDN JSON: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON
