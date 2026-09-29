# Lesson 01: JavaScript Foundations and Mental Models

## Goals

- Understand what JavaScript is and where it runs.
- Build a strong mental model for values, variables, expressions, and types.
- Learn why JavaScript feels different from many other languages.

## Prerequisites

- Basic comfort with programming concepts like variables and conditionals.

## Concepts

JavaScript is a general-purpose language used in browsers, servers, tooling, and build systems. A useful first mental model is this: JavaScript spends most of its time evaluating expressions, storing values in variables, and passing values into functions.

JavaScript values include strings, numbers, booleans, `null`, `undefined`, objects, arrays, and functions. Some of these are primitive values. Some are objects. This distinction matters because primitives behave like self-contained values, while objects are reference values.

`undefined` usually means "a value is missing right now." `null` usually means "we intentionally set this to no value." The language does not always enforce these meanings, but disciplined developers do.

## Worked Example

```js
const price = 19.99;
const taxRate = 0.08;
const total = price + price * taxRate;

console.log(total);
```

This code stores numeric values in `price` and `taxRate`, evaluates an arithmetic expression, and stores the result in `total`. JavaScript executes the right-hand side before assigning the final value.

Now compare that to object references:

```js
const user = { name: "Avery", role: "student" };
const sameUser = user;

sameUser.role = "junior developer";

console.log(user.role); // "junior developer"
```

## Explaining The Code

`sameUser = user` does not clone the object. It copies the reference. Both variables point at the same object in memory, so mutating through one variable changes what the other sees. This is one of the earliest JavaScript ideas that creates real bugs in app code.

## More Examples

```js
let score = 0;
score = score + 1;
score += 1;
```

Both updates increase the value. The second line is more explicit about the full reassignment process, while the third is shorthand.

```js
console.log(typeof "hello");     // string
console.log(typeof 42);          // number
console.log(typeof true);        // boolean
console.log(typeof undefined);   // undefined
console.log(typeof null);        // object (historical quirk)
console.log(typeof {});          // object
console.log(typeof []);          // object
console.log(typeof function(){});// function
```

The `typeof null` behavior is a famous historical bug. You do not need to like it, but you do need to know it exists.

## Practical Guidance

- Use `const` by default.
- Use `let` when reassignment is intentional.
- Avoid `var` in modern code unless you are reading legacy code.
- Treat arrays and objects as mutable containers unless you create a copy.

## Exercises

`Lab 01A`: Create variables for a product name, price, quantity, and whether it is on sale. Log a final summary string using template literals.

`Lab 01B`: Create an object called `profile`, assign it to another variable, mutate one property, and explain why both variables appear to change.

`Lab 01C`: Log the `typeof` result for five different values and write one sentence explaining each.

See the solution guide: [Lesson 01 Solutions](../../solutions/lesson-01-solutions.md)

## References

- MDN JavaScript Guide: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide
- MDN Grammar and Types: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types
- MDN JavaScript Overview: https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript

## Job-Readiness Takeaway

Junior engineers are constantly asked to inspect existing values, trace state changes, and understand why a variable does not contain what they expected. This lesson is simple on purpose because these core mental models are the base layer for almost every debugging task you will do later.
