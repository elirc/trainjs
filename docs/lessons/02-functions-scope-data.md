# Lesson 02: Control Flow, Functions, Scope, Closures, and Data Structures

## Goals

- Use conditionals and loops without losing readability.
- Understand function inputs, outputs, and side effects.
- Learn scope and closures well enough to explain them.
- Work productively with arrays and objects.
- Choose between `map`, `filter`, `find`, `some`, `every`, and `reduce` by the question you are asking.

## Prerequisites

- Lesson 01 or equivalent comfort with variables and types.
- Node.js for running the examples. The comments show the output each snippet should print with `node`; run them to confirm.

## Concepts

Control flow answers the question "what should the program do next?" Functions answer the question "how should this piece of logic be packaged?" Scope answers the question "which variables are available here?" Closures answer the question "why can this function still access that variable?"

Functions become much easier to reason about when you identify three things:

- what comes in
- what comes out
- what changes outside the function

### Pure functions and side effects

A function is **pure** when its output depends only on its inputs and it changes nothing outside itself. A **side effect** is any change the caller can observe besides the return value: mutating an argument or a shared object, writing to the screen, saving to storage, sending a request.

Side effects are not bad. Apps exist to cause them. The skill is keeping them in a few obvious places and keeping the decision-making logic pure, because pure logic is easy to test and reuse.

```js
const cart = { total: 0 };

function addToCartTotal(amount) {
  cart.total += amount;            // side effect: changes shared state
}

addToCartTotal(10);
addToCartTotal(10);
console.log(cart.total);           // 20

function withItemAdded(total, amount) {
  return total + amount;           // pure: same inputs, same output
}

console.log(withItemAdded(0, 10), withItemAdded(0, 10)); // 10 10
```

Calling `addToCartTotal(10)` twice gives a different result each time because it depends on hidden state. Calling `withItemAdded(0, 10)` twice gives `10` both times.

### Three ways to write a function

```js
function double(n) { return n * 2; }        // declaration
const doubleArrow = (n) => n * 2;           // arrow, implicit return
const doubleBlock = (n) => { return n * 2; }; // arrow with a body needs return
```

An arrow function with a single expression after `=>` returns that expression automatically. As soon as you add `{ }`, you must write `return`. Forgetting this is a classic bug:

```js
function doubleBroken(n) { n * 2; }
const doubleBlockBroken = (n) => { n * 2; };

console.log(doubleBroken(4), doubleBlockBroken(4)); // undefined undefined
```

A function without a `return` statement returns `undefined`.

### Scope

A variable is visible inside the block (`{ }`) where it is declared with `let` or `const`, and inside any blocks nested in it. Outer variables are visible to inner code; inner variables are not visible outside.

```js
const appName = "Tasks";

function show() {
  const message = `Welcome to ${appName}`; // outer variable is visible
  if (true) {
    const inner = "block only";
    console.log(inner);                    // block only
  }
  console.log(inner);                      // ReferenceError: inner is not defined
  return message;
}
```

When JavaScript looks up a name, it starts in the current block and walks outward until it finds a declaration. If it reaches the outermost scope without finding one, you get a `ReferenceError`.

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

Notice the shape: the special case is handled first and returns early, and the normal case sits at the bottom without an `else`. This "guard clause" style keeps nesting shallow. Also notice that floating point from Lesson 01 still applies: `calculateDiscount(19.99, true)` prints `17.991`, so a real checkout would round to cents.

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

Each call to `makeCounter` creates a **new** `count`:

```js
const other = makeCounter();
console.log(other(), counter()); // 1 3
```

`other` starts at 1 because it has its own `count`. `counter` continues from 2 to 3. Two closures, two private variables. Nothing outside can read or reset `count` directly, which is why closures are also a simple way to keep data private.

### The loop closure trap

```js
const fnsVar = [];
for (var i = 0; i < 3; i++) {
  fnsVar.push(() => i);
}
console.log(fnsVar.map(f => f())); // [ 3, 3, 3 ]

const fnsLet = [];
for (let j = 0; j < 3; j++) {
  fnsLet.push(() => j);
}
console.log(fnsLet.map(f => f())); // [ 0, 1, 2 ]
```

With `var`, there is one `i` for the whole function, and every closure sees its final value, `3`. With `let`, each loop iteration gets its own `j`. You will meet the `var` version in older code, and this exact behaviour is a common interview question.

## Arrays And Transformation

```js
const tasks = [
  { id: 1, done: false },
  { id: 2, done: true },
  { id: 3, done: false }
];

const incomplete = tasks.filter(task => !task.done);
console.log(incomplete);                    // [ { id: 1, done: false }, { id: 3, done: false } ]
console.log(tasks.length, incomplete.length); // 3 2
```

`filter` returns a new array containing only matching items. It does not change the original array. Methods like `map`, `filter`, and `find` are common in production code because they express intent clearly.

Pick the method by the question you are asking:

| Question | Method | Returns |
| --- | --- | --- |
| "Transform every item" | `map` | new array, same length |
| "Keep only some items" | `filter` | new array, same or shorter |
| "Give me the first match" | `find` | one item or `undefined` |
| "Is there at least one?" | `some` | boolean |
| "Do all of them match?" | `every` | boolean |
| "Combine into one value" | `reduce` | anything (a number, an object...) |

```js
const products = [
  { name: "Mouse", price: 25, inStock: true },
  { name: "Monitor", price: 180, inStock: false },
  { name: "Cable", price: 8, inStock: true }
];

console.log(products.map(p => p.name));          // [ 'Mouse', 'Monitor', 'Cable' ]
console.log(products.find(p => p.price > 100));  // { name: 'Monitor', price: 180, inStock: false }
console.log(products.find(p => p.price > 1000)); // undefined
console.log(products.some(p => !p.inStock), products.every(p => p.price > 5)); // true true
console.log(products.reduce((sum, p) => sum + p.price, 0)); // 213

const inStockTotal = products
  .filter(p => p.inStock)
  .map(p => p.price)
  .reduce((sum, price) => sum + price, 0);
console.log(inStockTotal); // 33
```

The chained version reads like a sentence: keep the in-stock products, take their prices, add them up. Always give `reduce` a starting value (the `0`); without it, `reduce` on an empty array throws a `TypeError`.

### Methods that change the original

Not every array method returns a new array. `push`, `pop`, `splice`, `reverse`, and `sort` change the array in place.

```js
const prices = [10, 9, 1, 100];
const sorted = prices.sort();
console.log(sorted, prices, sorted === prices); // [ 1, 10, 100, 9 ] [ 1, 10, 100, 9 ] true

const nums = [10, 9, 1, 100];
console.log([...nums].sort((a, b) => a - b), nums); // [ 1, 9, 10, 100 ] [ 10, 9, 1, 100 ]
```

Two surprises in one example. `sort()` with no comparator compares items as **strings**, so `"100"` comes before `"9"`. And it sorts the original array, so `sorted` and `prices` are the same array. Copy first and pass a comparator. Node 20 and later also have `toSorted`, which returns a sorted copy.

## Objects As Data

```js
const user = { name: "Avery", role: "student" };

console.log(Object.keys(user));    // [ 'name', 'role' ]
console.log(Object.entries(user)); // [ [ 'name', 'Avery' ], [ 'role', 'student' ] ]

for (const [key, value] of Object.entries(user)) {
  console.log(`${key}=${value}`);  // name=Avery, then role=student
}

const promoted = { ...user, role: "junior developer" };
console.log(user.role, promoted.role); // student junior developer

const { name, role: currentRole } = promoted;
console.log(name, currentRole);        // Avery junior developer
```

`{ ...user, role: "junior developer" }` copies every property and then overrides `role`, leaving the original alone. This "copy and override" pattern is exactly how React state updates are written in Lesson 10. Destructuring (`const { name } = promoted`) pulls properties into variables, and `role: currentRole` renames one on the way.

## Control Flow Patterns

```js
function shippingCost(total) {
  if (total <= 0) return 0;
  if (total >= 50) return 0;
  return 5;
}
console.log(shippingCost(0), shippingCost(20), shippingCost(50)); // 0 5 0

function statusLabel(status) {
  switch (status) {
    case "todo": return "To do";
    case "doing": return "In progress";
    case "done": return "Done";
    default: return "Unknown";
  }
}
console.log(statusLabel("doing"), statusLabel("archived")); // In progress Unknown

for (const p of products) {
  if (!p.inStock) continue;
  console.log(p.name);   // Mouse, then Cable
}
```

- A chain of early returns is often clearer than nested `if/else`.
- `switch` fits "one value, several fixed cases". Always include a `default`.
- `for...of` iterates values of arrays (and strings, maps, sets). `continue` skips to the next item; `break` stops the loop.
- Test the boundaries: `shippingCost(50)` is free because the check is `>=`. Off-by-one errors live at boundaries.

## Parameters: Defaults And Rest

```js
function greet(name = "friend") {
  return `Hi, ${name}`;
}
console.log(greet(), greet(undefined), greet(null), greet("Sam")); // Hi, friend Hi, friend Hi, null Hi, Sam

function sum(...numbers) {
  return numbers.reduce((s, n) => s + n, 0);
}
console.log(sum(1, 2, 3), sum()); // 6 0
```

A default parameter is used only when the argument is `undefined` (missing or passed explicitly). `null` is a real value, so `greet(null)` prints `Hi, null`. Rest parameters (`...numbers`) collect any number of arguments into a real array.

## Explaining The Code

The counter example matters because it shows that functions are not just reusable code blocks. They also carry access to the environment where they were created. This is why a bug inside a callback can depend on variables that were declared much earlier.

Put the pieces of this lesson together and you have the vocabulary to read most everyday code: a function receives inputs (parameters with defaults), makes a decision (guard clauses, `switch`), transforms data (`filter`, `map`, `reduce`), and either returns a result or causes a side effect. Closures explain how a callback written in one place can still use variables from another.

## More Examples

`Set` and `Map` are built-in data structures that come up often:

```js
const tags = ["js", "react", "js", "node"];
console.log([...new Set(tags)]); // [ 'js', 'react', 'node' ]

const counts = new Map();
for (const t of tags) {
  counts.set(t, (counts.get(t) ?? 0) + 1);
}
console.log(counts.get("js"), counts.size); // 2 3
```

A `Set` stores each value once, which makes removing duplicates a one-liner. A `Map` is a key-value store whose keys can be any type, with a reliable `size`. The `?? 0` uses the default operator from Lesson 01, because `counts.get` returns `undefined` for a key that is not there yet.

## Practical Guidance

- Name functions after what they return or do: `getGrade`, `isInStock`, `formatPrice`.
- Keep decision logic in pure functions; keep side effects at the edges.
- Prefer `const` plus array methods over manual index loops when you are transforming data.
- Use `for...of` when you need `break`, `continue`, or `await` inside the loop.
- Copy before you sort or reverse, unless changing the original is the point.
- Give `reduce` an initial value.

## Common Mistakes

- **Forgetting `return`** in a function body or an arrow function with braces. The result is `undefined`.
- **Using `map` for side effects** (for example, only to `console.log`). Use `forEach` or `for...of`; `map` is for building a new array.
- **Expecting `find` to return an array.** It returns one item or `undefined`. Check for `undefined` before reading properties.
- **Sorting numbers without a comparator.** `[10, 9, 1, 100].sort()` gives `[1, 10, 100, 9]`.
- **Mutating an argument by accident**, such as calling `items.sort()` on an array the caller still uses.
- **Assuming each closure gets its own copy of a `var` loop variable.** Use `let`.

## Check Yourself

1. What does `[1, 2, 3].map(n => { n * 2 })` return?
2. `const c1 = makeCounter(); const c2 = makeCounter(); c1(); c1(); console.log(c2());` prints what?
3. Which method answers "is any task overdue?"
4. What is `[].reduce((s, n) => s + n, 0)`?
5. What is the difference between `greet(undefined)` and `greet(null)` for `function greet(name = "friend")`?

Answers:

1. `[ undefined, undefined, undefined ]`. The braces make it a function body with no `return`.
2. `1`. `c2` has its own `count`.
3. `some`.
4. `0`, the initial value. Without the `0` it would throw.
5. `undefined` triggers the default (`Hi, friend`); `null` does not (`Hi, null`).

## Exercises

`Lab 02A`: Write a function `getGrade(score)` that returns `"A"`, `"B"`, `"C"`, `"D"`, or `"F"`.

- Decide and document what happens at the boundaries (exactly 90, exactly 60) and for invalid input such as `-5`, `150`, or `"ninety"`.

`Lab 02B`: Write a function factory called `makeGreeter(name)` that returns a function which greets that person later.

- Create two greeters and show that each remembers its own name.

`Lab 02C`: Given an array of product objects, return a new array that contains only products currently in stock.

- Show that the original array still has every product afterwards.

`Lab 02D`: Explain the difference between a function that returns a value and a function that mutates an external object.

- Write one small example of each.

See the solution guide: [Lesson 02 Solutions](../../solutions/lesson-02-solutions.md)

## References

- MDN Functions: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions
- MDN Closures: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Closures
- MDN Indexed Collections: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections
- MDN Keyed Collections (`Map`, `Set`): https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Keyed_collections
- MDN `Array.prototype.sort()`: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

## Job-Readiness Takeaway

Real product code is mostly functions moving values around. If you can read a function signature, trace scope, and transform arrays safely, you can contribute to frontend and backend code far earlier than you might think.

In a code review, the questions you can now ask are the ones reviewers actually ask: "Does this function have a side effect the name hides?", "Is this `sort` changing an array someone else holds?", "What happens when `find` returns `undefined`?". Asking them about your own code before you open a pull request is one of the habits that separates someone who can be trusted with changes from someone who needs every change checked line by line.
