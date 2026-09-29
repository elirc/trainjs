# Lesson 09: TypeScript for JavaScript Developers

## Goals

- Understand what TypeScript adds to JavaScript.
- Add types to familiar JavaScript patterns.
- Use TypeScript as a tool for clarity, not a replacement for understanding.

## Prerequisites

- Solid comfort with JavaScript functions, objects, arrays, and modules.

## Concepts

TypeScript is JavaScript plus static analysis and a type system. It helps catch mismatches earlier, especially in growing codebases with many files and contributors.

TypeScript does not make bad logic good, but it can reveal incorrect assumptions. That is the mindset you want: types are feedback.

## Worked Example

```ts
type Task = {
  id: number;
  title: string;
  done: boolean;
};

function formatTask(task: Task): string {
  return `${task.done ? "x" : " "} ${task.title}`;
}

const task: Task = {
  id: 1,
  title: "Write tests",
  done: false
};

console.log(formatTask(task));
```

## Explaining The Code

The `Task` type describes the shape of objects this function expects. If you pass an object missing `title` or using the wrong value type, TypeScript can warn you before runtime.

That is the main win for beginners: fewer silent mistakes around object shape and function contracts.

## JavaScript To TypeScript Migration Pattern

Start small:

1. rename one file from `.js` to `.ts`
2. add parameter and return types to important functions
3. type shared objects and API responses
4. fix the most helpful errors first

Avoid trying to type every advanced edge case immediately.

## Exercises

`Lab 09A`: Convert a JavaScript `user` object shape into a TypeScript `type`.

`Lab 09B`: Add types to a function that filters in-stock products.

`Lab 09C`: Write two sentences explaining why TypeScript helps with API data and refactors.

See the solution guide: [Lesson 09 Solutions](../../solutions/lesson-09-solutions.md)

## References

- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro
- TypeScript for JavaScript Programmers: https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html
- MDN JavaScript Guide: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide

## Job-Readiness Takeaway

Many junior roles increasingly expect at least beginner TypeScript literacy. You do not need advanced type wizardry. You do need to read typed code, add basic types, and understand why teams adopt it.
