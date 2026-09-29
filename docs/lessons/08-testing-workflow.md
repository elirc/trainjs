# Lesson 08: Testing, Code Quality, Debugging Workflow, and Junior Habits

## Goals

- Write small tests around useful logic.
- Understand what to test first as a beginner.
- Build a debugging workflow that scales beyond guesswork.
- Learn habits that make code review easier.

## Prerequisites

- Lessons 01-07.

## Concepts

Testing is not about proving code is perfect. It is about reducing uncertainty. As a junior engineer, the easiest high-value tests usually target:

- pure functions
- validation logic
- small utility helpers
- route behavior for happy path and obvious failures

## Worked Example

```js
import { strict as assert } from "node:assert";
import test from "node:test";

function isValidEmail(email) {
  return email.includes("@") && email.includes(".");
}

test("accepts a normal email", () => {
  assert.equal(isValidEmail("dev@example.com"), true);
});

test("rejects a malformed email", () => {
  assert.equal(isValidEmail("not-an-email"), false);
});
```

## Explaining The Code

This example uses Node's built-in test runner to check a small pure function. The tests are easy to read because the function has one job and no hidden external state. That is another reason pure functions are so valuable.

## Debugging Workflow

When debugging, avoid random changes. Use a repeatable process:

1. reproduce the bug reliably
2. describe expected behavior in one sentence
3. inspect actual inputs and outputs
4. narrow the failing layer: UI, state, network, server, or data
5. fix one thing at a time
6. re-test the original reproduction path

## Code Quality Habits

- choose descriptive names
- keep functions focused
- return early when that reduces nesting
- write comments only when the intent would otherwise be hard to infer
- avoid clever abstractions before the problem is repeated

## Exercises

`Lab 08A`: Write tests for a `calculateTotal(items)` function.

`Lab 08B`: Write tests for the validation logic in a route or form.

`Lab 08C`: Take a bug you have hit in earlier lessons and document the debugging steps you would use now.

See the solution guide: [Lesson 08 Solutions](../../solutions/lesson-08-solutions.md)

## References

- Jest Docs: https://jestjs.io/help
- Node.js Test Runner Docs: https://nodejs.org/api/test.html
- MDN Debugging JavaScript: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/What_went_wrong

## Job-Readiness Takeaway

Teams do not just want code that works once. They want code that is understandable, fixable, and safer to change. Testing and debugging discipline are what turn "I think it works" into "I checked it and can explain why."
