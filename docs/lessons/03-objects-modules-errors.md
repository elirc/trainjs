# Lesson 03: Objects, Prototypes, Classes, Modules, and Error Handling

## Goals

- Understand how JavaScript models objects and shared behavior.
- Learn the difference between object literals, prototypes, and classes.
- Organize code with modules.
- Handle failures intentionally instead of letting code crash mysteriously.

## Prerequisites

- Lesson 02, especially functions and scope.

## Concepts

Objects group related data and behavior. In JavaScript, objects inherit behavior through the prototype chain. Classes give a cleaner syntax for a pattern that still uses prototypes underneath.

Modules help split programs into focused files with clear exports and imports. As your code grows, module boundaries matter as much as correct syntax.

Error handling is part of normal programming, not an advanced bonus topic. Good developers assume failures will happen and define what the program should do next.

## Worked Example

```js
class Cart {
  constructor() {
    this.items = [];
  }

  addItem(name, price) {
    this.items.push({ name, price });
  }

  getTotal() {
    return this.items.reduce((sum, item) => sum + item.price, 0);
  }
}

const cart = new Cart();
cart.addItem("Notebook", 8);
cart.addItem("Pen", 2);

console.log(cart.getTotal()); // 10
```

## Explaining The Code

The `Cart` class is syntactic sugar over prototypes. Methods like `addItem` and `getTotal` are shared through the class prototype rather than recreated on every instance. You do not have to hand-write the prototype chain often, but you should know classes are not magic.

## Modules Example

```js
// math.js
export function double(value) {
  return value * 2;
}

// app.js
import { double } from "./math.js";

console.log(double(4));
```

Modules reduce hidden global state and make reuse explicit.

## Error Handling Example

```js
function parseUser(jsonString) {
  try {
    const user = JSON.parse(jsonString);

    if (!user.name) {
      throw new Error("User must have a name");
    }

    return user;
  } catch (error) {
    console.error("Failed to parse user:", error.message);
    return null;
  }
}
```

This function handles two failure modes: invalid JSON and missing required data.

## Exercises

`Lab 03A`: Build a `BankAccount` class with `deposit`, `withdraw`, and `getBalance` methods.

`Lab 03B`: Split a small utility into two modules and import one into the other.

`Lab 03C`: Write a function that safely parses JSON and returns a default value when parsing fails.

See the solution guide: [Lesson 03 Solutions](../../solutions/lesson-03-solutions.md)

## References

- MDN Working With Objects: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_objects
- MDN Prototype Chain: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
- MDN JavaScript Modules: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

## Job-Readiness Takeaway

By this point, you are beginning to think in application structure rather than isolated snippets. That shift matters in a junior role because most tasks are changes inside an existing codebase, not greenfield toy scripts.
