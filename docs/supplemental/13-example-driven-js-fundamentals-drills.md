# Example-Driven JavaScript Fundamentals Drills

## How To Use This Guide

This file is for repetition. The goal is not to race through it. The goal is to make basic JavaScript behavior feel normal.

For each example:

1. Read the code only.
2. Predict the output or result.
3. Explain why in one or two sentences.
4. Then read the breakdown.
5. Change one line and test your new prediction.

This guide stays focused on plain JavaScript fundamentals. No React, no backend architecture, no framework setup. Just the language and the habits needed to read it fluently.

## Section 1: Variables, Reassignment, and Basic Values

### Example 1

```js
let count = 1;
count = count + 1;

console.log(count);
```

This logs `2`.

Explanation:

- `count` starts as `1`.
- `count + 1` evaluates to `2`.
- The result is reassigned back into `count`.

This pattern shows up constantly in counters, totals, and loop logic.

### Example 2

```js
const name = "Sam";
console.log(name);
```

This logs `"Sam"`.

Explanation:

- `const` means the variable name cannot be reassigned.
- It does not mean the value is magically frozen in all cases.

Many beginners hear “constant” and think it means “fully immutable.” That is not true for objects and arrays.

### Example 3

```js
const user = { name: "Sam" };
user.name = "Jordan";

console.log(user.name);
```

This logs `"Jordan"`.

Explanation:

- `user` is still pointing to the same object.
- Changing a property mutates the object.
- `const` prevents `user = anotherObject`, but it does not block object mutation.

## Section 2: Strings, Numbers, and Operators

### Example 4

```js
console.log("5" + 2);
```

This logs `"52"`.

Explanation:

- When `+` sees a string, JavaScript often performs string concatenation.
- The number `2` is converted to the string `"2"`.

This is why type awareness matters even in tiny expressions.

### Example 5

```js
console.log("5" - 2);
```

This logs `3`.

Explanation:

- `-` is numeric subtraction, not string concatenation.
- JavaScript converts `"5"` into the number `5`.

The same value can behave differently depending on the operator.

### Example 6

```js
console.log(2 + 3 * 4);
```

This logs `14`.

Explanation:

- Multiplication happens before addition.
- `3 * 4` becomes `12`.
- Then `2 + 12` becomes `14`.

When in doubt, add parentheses to make intent obvious.

### Example 7

```js
const price = 19.99;
const message = `The total is $${price}`;

console.log(message);
```

Explanation:

- Template literals use backticks.
- `${price}` injects the current value into the string.

This is cleaner than long chains of string concatenation in most app code.

## Section 3: Truthiness and Conditionals

### Example 8

```js
if ("hello") {
  console.log("runs");
}
```

This logs `"runs"`.

Explanation:

- Non-empty strings are truthy.
- Truthy does not mean “literally `true`.”
- It means “behaves like true in a conditional.”

### Example 9

```js
if (0) {
  console.log("runs");
} else {
  console.log("skips");
}
```

This logs `"skips"`.

Explanation:

- `0` is falsy.
- Falsy values are special values that behave like `false` in conditions.

Important falsy values to know:

- `false`
- `0`
- `""`
- `null`
- `undefined`
- `NaN`

### Example 10

```js
const role = "admin";

if (role === "admin") {
  console.log("full access");
}
```

Explanation:

- `===` checks strict equality.
- Both value and type must match.

Use `===` by default in modern JavaScript unless you have a specific reason not to.

### Example 11

```js
console.log(5 == "5");
console.log(5 === "5");
```

This logs `true` and then `false`.

Explanation:

- `==` allows type coercion before comparing.
- `===` compares without coercion.

This is one of the classic reasons strict equality is safer and easier to reason about.

## Section 4: Functions and Return Values

### Example 12

```js
function double(value) {
  return value * 2;
}

console.log(double(4));
```

This logs `8`.

Explanation:

- `value` is the input.
- `return` sends the result back to the caller.

Try to describe functions in this format:

- input
- output
- side effects

### Example 13

```js
function sayHi(name) {
  console.log(`Hi, ${name}`);
}

const result = sayHi("Avery");
console.log(result);
```

Explanation:

- The function logs a greeting as a side effect.
- It does not explicitly return a value.
- Functions without a return value return `undefined`.

That is why `result` becomes `undefined`.

### Example 14

```js
function multiply(a, b = 2) {
  return a * b;
}

console.log(multiply(5));
```

This logs `10`.

Explanation:

- `b = 2` is a default parameter.
- If the caller does not provide a second argument, `b` uses `2`.

Default parameters reduce repetitive guard code in many functions.

### Example 15

```js
const subtract = (a, b) => a - b;
console.log(subtract(10, 3));
```

This logs `7`.

Explanation:

- This is an arrow function.
- With one expression and no braces, the result is returned implicitly.

Arrow functions are common, but they are still just functions with a slightly different syntax and behavior.

## Section 5: Scope and Closures

### Example 16

```js
const topic = "global";

function showTopic() {
  const topic = "local";
  console.log(topic);
}

showTopic();
console.log(topic);
```

This logs `"local"` and then `"global"`.

Explanation:

- The inner `topic` shadows the outer one inside the function.
- Outside the function, the global `topic` still exists.

Scope answers the question: which variable does this piece of code see from here?

### Example 17

```js
function createGreeter(name) {
  return function () {
    return `Hello, ${name}`;
  };
}

const greetSam = createGreeter("Sam");
console.log(greetSam());
```

Explanation:

- The returned function still has access to `name`.
- That preserved access is closure.

Closures are not rare. They show up in factories, callbacks, and UI logic constantly.

## Section 6: Arrays and Looping

### Example 18

```js
const colors = ["red", "blue", "green"];
console.log(colors[1]);
```

This logs `"blue"`.

Explanation:

- Array indexes start at `0`.
- Index `1` is the second item.

### Example 19

```js
const numbers = [1, 2, 3];
numbers.push(4);

console.log(numbers);
```

Explanation:

- `push` mutates the array by adding a new item at the end.

This is fine in plain scripts, but in state-driven UI code you often prefer non-mutating patterns.

### Example 20

```js
for (let i = 0; i < 3; i += 1) {
  console.log(i);
}
```

This logs `0`, `1`, and `2`.

Explanation:

- `i = 0` sets the starting value.
- `i < 3` is checked before each loop run.
- `i += 1` runs after each iteration.

Say the loop in English:

- start at 0
- keep going while less than 3
- increase by 1 each time

### Example 21

```js
const names = ["Mia", "Leo", "Nina"];

for (const name of names) {
  console.log(name);
}
```

Explanation:

- `for...of` loops over values directly.
- This is often easier to read than manual index loops when you do not need the index.

### Example 22

```js
const values = [2, 4, 6];
const doubled = values.map(value => value * 2);

console.log(doubled);
```

This logs `[4, 8, 12]`.

Explanation:

- `map` creates a new array.
- Each item is transformed by the callback.

Think of `map` as “same number of items, different values.”

### Example 23

```js
const scores = [40, 75, 90, 55];
const passing = scores.filter(score => score >= 60);

console.log(passing);
```

This logs `[75, 90]`.

Explanation:

- `filter` keeps only items that pass a condition.
- The original array stays unchanged.

Think of `filter` as “fewer items, same shape.”

## Section 7: Objects and Property Access

### Example 24

```js
const product = {
  name: "Notebook",
  price: 12
};

console.log(product.name);
```

Explanation:

- Dot notation reads a property from an object.
- Objects are a way to group related values under named keys.

### Example 25

```js
const key = "price";
console.log(product[key]);
```

Explanation:

- Bracket notation is useful when the property name is stored in a variable.
- `product[key]` looks up the value under `"price"`.

### Example 26

```js
const item = { name: "Pen", stock: 10 };
const updatedItem = { ...item, stock: 9 };

console.log(item.stock, updatedItem.stock);
```

This logs `10 9`.

Explanation:

- The spread operator makes a new top-level object.
- `updatedItem` gets a changed `stock` value.
- `item` stays unchanged.

This pattern is central to immutable updates.

## Section 8: Destructuring and Rest Patterns

### Example 27

```js
const user = {
  name: "Jamie",
  role: "developer"
};

const { name, role } = user;
console.log(name, role);
```

Explanation:

- Destructuring pulls properties into variables.
- `name` gets `user.name`.
- `role` gets `user.role`.

This is common in function parameters and React props.

### Example 28

```js
const [first, second] = ["a", "b", "c"];
console.log(first, second);
```

This logs `"a b"`.

Explanation:

- Array destructuring matches values by position.
- Only the first two items are assigned here.

### Example 29

```js
const [head, ...rest] = [1, 2, 3, 4];
console.log(head, rest);
```

This logs `1 [2, 3, 4]`.

Explanation:

- `head` gets the first item.
- `...rest` collects the remaining items into a new array.

This pattern is useful when you need one part of an array and want to keep the remainder.

## Section 9: Short-Circuiting and Safe Access

### Example 30

```js
const savedName = "" || "Anonymous";
console.log(savedName);
```

This logs `"Anonymous"`.

Explanation:

- `||` returns the first truthy value it finds.
- `""` is falsy, so JavaScript moves to `"Anonymous"`.

This is useful, but be careful: sometimes `0` or `""` are valid values and should not be replaced.

### Example 31

```js
const count = 0 ?? 10;
console.log(count);
```

This logs `0`.

Explanation:

- `??` only falls back for `null` or `undefined`.
- Since `0` is a real value here, it is kept.

This is often safer than `||` for numeric counts and intentionally empty strings.

### Example 32

```js
const profile = null;
console.log(profile?.name);
```

This logs `undefined`.

Explanation:

- Optional chaining safely stops if the left side is `null` or `undefined`.
- Without it, `profile.name` would throw an error.

This is helpful for nested data that may not exist yet.

## Section 10: Array Methods for Real Work

### Example 33

```js
const team = [
  { name: "Ava", role: "dev" },
  { name: "Noah", role: "designer" }
];

const dev = team.find(member => member.role === "dev");
console.log(dev);
```

Explanation:

- `find` returns the first matching item.
- If nothing matches, it returns `undefined`.

Use `find` when you want one item, not a whole filtered list.

### Example 34

```js
const cart = [
  { price: 10 },
  { price: 15 },
  { price: 5 }
];

const total = cart.reduce((sum, item) => sum + item.price, 0);
console.log(total);
```

This logs `30`.

Explanation:

- `reduce` combines many items into one result.
- `sum` is the running total.
- `0` is the initial accumulator value.

If `reduce` feels hard, slow it down and track both variables on paper.

## Section 11: Errors and Defensive Thinking

### Example 35

```js
function parseJson(text) {
  try {
    return JSON.parse(text);
  } catch (error) {
    return null;
  }
}
```

Explanation:

- `JSON.parse` throws if the text is invalid JSON.
- `try/catch` lets the program recover instead of crashing immediately.

Error handling is part of normal JavaScript, not an advanced side topic.

### Example 36

```js
function divide(a, b) {
  if (b === 0) {
    throw new Error("Cannot divide by zero");
  }

  return a / b;
}
```

Explanation:

- This function guards against invalid input.
- Throwing an error makes the failure explicit.

Good code is not only code that works on the happy path. It also handles bad input intentionally.

## Section 12: Mini Reading Drills

Try these without looking ahead.

### Drill 1

```js
const numbers = [1, 2, 3];
const result = numbers.map(n => n + 1).filter(n => n > 2);

console.log(result);
```

Expected result:

- `[3, 4]`

Why:

- `map` turns `[1, 2, 3]` into `[2, 3, 4]`
- `filter` keeps only values greater than `2`

### Drill 2

```js
const config = { retries: 0 };
const retries = config.retries || 3;

console.log(retries);
```

Expected result:

- `3`

Why:

- `0` is falsy
- `||` falls through to `3`

This is a good reminder that `||` is sometimes too aggressive for defaults.

### Drill 3

```js
const config = { retries: 0 };
const retries = config.retries ?? 3;

console.log(retries);
```

Expected result:

- `0`

Why:

- `??` only falls back for `null` or `undefined`
- `0` is kept

## Section 13: Practice Prompts

Use the patterns in this file to write your own tiny examples for:

- a function with a default parameter
- an object update using spread
- a `map` plus `filter` chain
- a `find` call on an array of objects
- a safe access example using optional chaining
- a `try/catch` wrapper around risky input

You will learn faster if you write your own two-line and three-line drills instead of only reading mine.

## References

- MDN JavaScript Guide: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide
- MDN Expressions and Operators: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_operators
- MDN Functions: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions
- MDN Working With Objects: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_objects
- MDN Indexed Collections: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections

## Takeaway

Strong JavaScript fundamentals are not built by reading one giant explanation once. They are built by seeing small patterns repeatedly until those patterns stop feeling surprising.

If the main course gives you the structured path and the first supplemental file gives you JS/React pattern practice, this drill file is here to strengthen the smallest building blocks until they feel automatic.
