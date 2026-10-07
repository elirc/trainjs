# Lesson 01: JavaScript Foundations and Mental Models

## Goals

- Understand what JavaScript is and where it runs.
- Build a strong mental model for values, variables, expressions, and types.
- Learn why JavaScript feels different from many other languages.
- Predict what a short snippet prints before you run it, and explain any surprise afterwards.

## Prerequisites

- Basic comfort with programming concepts like variables and conditionals.
- Node.js installed, so you can run the examples. Save a snippet as `example.mjs` and run `node example.mjs`. The comments in each snippet show the output you should see in a current Node version; if yours differs, that difference is worth investigating.

## Concepts

JavaScript is a general-purpose language used in browsers, servers, tooling, and build systems. A useful first mental model is this: JavaScript spends most of its time evaluating expressions, storing values in variables, and passing values into functions.

### Where JavaScript runs

The language itself is the same everywhere: variables, functions, objects, `if`, loops. What changes is the environment around it.

- In a browser, you also get `document`, `window`, `localStorage`, and the DOM (Lesson 04).
- In Node.js, you get `process`, the file system, and network servers (Lesson 06).
- In both, you get `console.log`, timers, `JSON`, `Math`, and the core language.

When a tutorial uses `document.querySelector` and your Node script says `document is not defined`, that is not a language bug. It is the wrong environment.

### Values and types

JavaScript values include strings, numbers, booleans, `null`, `undefined`, objects, arrays, and functions. There are also two less common primitives, `bigint` and `symbol`. Some of these are primitive values. Some are objects. This distinction matters because primitives behave like self-contained values, while objects are reference values.

| Kind | Examples | Copying a variable copies... |
| --- | --- | --- |
| Primitive | `"hi"`, `42`, `true`, `null`, `undefined`, `10n`, `Symbol("id")` | the value itself |
| Object (reference) | `{}`, `[]`, functions, dates, maps | a reference to the same object |

### Variables are labels, not boxes

A helpful picture: a variable is a label that points at a value. For a primitive, two labels never share anything you can change, because primitives cannot be changed in place. For an object, two labels can point at the same object, and a change made through one label is visible through the other.

### `undefined` and `null`

`undefined` usually means "a value is missing right now." `null` usually means "we intentionally set this to no value." The language does not always enforce these meanings, but disciplined developers do.

You get `undefined` without asking for it: a declared but unassigned variable, a missing object property, a function with no `return`. You only get `null` when some code chooses to put it there.

### Expressions and statements

An expression produces a value: `price * taxRate`, `user.role`, `count > 3`. A statement does something: `const total = ...;`, `if (...) { ... }`. Most debugging questions come down to "what value did this expression produce?" That is why `console.log` is your first debugging tool.

## Worked Example

```js
const price = 19.99;
const taxRate = 0.08;
const total = price + price * taxRate;

console.log(total);            // 21.589199999999998
console.log(total.toFixed(2)); // 21.59
```

This code stores numeric values in `price` and `taxRate`, evaluates an arithmetic expression, and stores the result in `total`. JavaScript executes the right-hand side before assigning the final value. Multiplication runs before addition, so this is `19.99 + (19.99 * 0.08)`.

The first line of output surprises most people. JavaScript numbers are 64-bit floating-point values, and many decimal fractions (like `0.08`) cannot be stored exactly in binary. The tiny error shows up when you print the raw result. `toFixed(2)` rounds it for display, and it returns a **string**, not a number (`typeof total.toFixed(2)` is `"string"`).

Now compare that to object references:

```js
const user = { name: "Avery", role: "student" };
const sameUser = user;

sameUser.role = "junior developer";

console.log(user.role);          // "junior developer"
console.log(user === sameUser);  // true
```

## Explaining The Code

`sameUser = user` does not clone the object. It copies the reference. Both variables point at the same object in memory, so mutating through one variable changes what the other sees. This is one of the earliest JavaScript ideas that creates real bugs in app code.

`user === sameUser` is `true` because `===` on objects asks "is this the same object?", not "do these objects contain the same data?". Two separately created objects are never equal, even with identical contents:

```js
console.log({} === {}); // false
```

Primitives behave differently:

```js
let a = 5;
let b = a;
b = 6;

console.log(a, b); // 5 6
```

`b = a` copies the number `5`. Reassigning `b` points the label `b` at a new value and leaves `a` alone.

### Making a real copy

If you need an independent object, create one:

```js
const original = { name: "Sam", address: { city: "Austin" } };

const shallow = { ...original };
shallow.name = "Riley";
shallow.address.city = "Denver";

console.log(original.name, original.address.city); // Sam Denver

const deep = structuredClone(original);
deep.address.city = "Boston";

console.log(original.address.city, deep.address.city); // Denver Boston
```

The spread copy `{ ...original }` is **shallow**. It creates a new outer object, so changing `shallow.name` did not touch `original.name`. But `address` is itself an object, and only its reference was copied, so changing `shallow.address.city` also changed `original.address.city`. `structuredClone` (available in modern browsers and in Node 17 and later) copies nested data as well.

## More Examples

### Updating a variable

```js
let score = 0;
score = score + 1;
score += 1;
```

Both updates increase the value. The second line is more explicit about the full reassignment process, while the third is shorthand. After both lines, `score` is `2`.

### `typeof`

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

The `typeof null` behavior is a famous historical bug. You do not need to like it, but you do need to know it exists. Arrays also report `"object"`, so use `Array.isArray(value)` when you need to know whether something is an array (`Array.isArray([])` is `true`, `Array.isArray({})` is `false`).

### `const` does not freeze objects

```js
const settings = { theme: "light" };
settings.theme = "dark";
console.log(settings.theme); // dark

const limit = 1;
limit = 2; // TypeError: Assignment to constant variable.
```

`const` means the **label** cannot be pointed somewhere else. It says nothing about whether the object it points to can change.

### Equality: use `===`

```js
console.log(0 == "", 0 === "");                  // true false
console.log(null == undefined, null === undefined); // true false
console.log("1" == 1, "1" === 1);                // true false
console.log(NaN === NaN, Number.isNaN(NaN));     // false true
```

`==` converts types before comparing, which produces results that are hard to predict. `===` compares without conversion. Use `===` by default. `NaN` ("not a number") is the one value that is not equal to itself, so check for it with `Number.isNaN`.

### Type coercion

```js
console.log("5" + 1);              // 51
console.log("5" - 1);              // 4
console.log(Number(""), Number("  42 "), Number("abc")); // 0 42 NaN
console.log(Number.parseInt("42px", 10), Number("42px")); // 42 NaN
```

`+` with a string on either side means string concatenation, so `"5" + 1` is `"51"`. `-` only works on numbers, so `"5" - 1` converts the string and gives `4`. This is why form values, which always arrive as strings, must be converted on purpose before you do arithmetic. Note that `Number("")` is `0`, not `NaN`, which is a common source of "empty field counted as zero" bugs.

### Money and floating point

```js
console.log(0.1 + 0.2);         // 0.30000000000000004
console.log(0.1 + 0.2 === 0.3); // false

const priceCents = 1999;
const taxCents = Math.round(priceCents * 0.08);
console.log(priceCents + taxCents, ((priceCents + taxCents) / 100).toFixed(2)); // 2159 21.59
```

For money, a common approach is to store whole cents as integers, round once at a defined point, and format only for display.

### Truthy and falsy

In an `if` condition, every value is treated as true or false. These are the falsy values:

```js
// false for: 0, "", null, undefined, NaN, false
// true for:  "0", " ", [], {}, -1   (and every other value)
```

You can confirm any of them with `Boolean(value)`. Empty arrays and empty objects are truthy, which surprises people who expect `if (items)` to mean "if there are items". Use `items.length > 0` for that.

### Defaults: `||` versus `??`

```js
const savedVolume = 0;
console.log(savedVolume || 50); // 50
console.log(savedVolume ?? 50); // 0
```

`||` falls back on any falsy value, so a real saved volume of `0` is thrown away. `??` (nullish coalescing) only falls back on `null` or `undefined`. When `0`, `""`, or `false` are valid values, use `??`.

### Missing values in practice

```js
let notYetSet;
const profile = { name: "Jordan" };
console.log(notYetSet, profile.age, profile.middleName === undefined); // undefined undefined true

const cleared = { nickname: null };
console.log(cleared.nickname, "nickname" in cleared, "age" in cleared); // null true false
```

`profile.age` is `undefined` because the property does not exist. `cleared.nickname` is `null` because someone set it on purpose. The `in` operator tells you whether the property exists at all.

### Reading through `null` safely

```js
const order = { customer: null };
console.log(order.customer?.email); // undefined
console.log(order.customer.email);  // TypeError: Cannot read properties of null (reading 'email')
```

That `TypeError` is probably the single most common runtime error in JavaScript apps. Optional chaining (`?.`) stops and returns `undefined` when the left side is `null` or `undefined`.

### Template literals

```js
const productName = "Desk Lamp";
const qty = 3;
console.log(`${qty} x ${productName} = $${(qty * 24.5).toFixed(2)}`); // 3 x Desk Lamp = $73.50
```

Backtick strings can embed any expression inside `${ }`. The `$$` is a literal dollar sign followed by an embedded expression.

## Debugging Walkthrough: "The total says 105"

A bug report says: "I ordered 10 items, added 5 more, and the cart shows 105." Here is a reduced version of the code:

```js
const quantityInput = "10";   // values read from a form are strings
const extraItems = 5;
const totalItems = quantityInput + extraItems;

console.log(totalItems); // 105
```

Work through it in the same order you will use for every bug in this course.

1. **Reproduce it.** Run the snippet. It prints `105`, so the bug is real and small enough to study.
2. **State the expected behaviour in one sentence.** "10 plus 5 should be 15."
3. **Inspect the actual values and their types.** Do not guess; log them.

   ```js
   console.log(totalItems, typeof totalItems);                                    // 105 string
   console.log(quantityInput, typeof quantityInput, extraItems, typeof extraItems); // 10 string 5 number
   ```

   The result is a string, and one input is a string. That explains everything: `+` with a string concatenates.
4. **Fix the cause, not the symptom.** Convert at the boundary where the string enters your code, and decide what happens when the conversion fails:

   ```js
   const quantity = Number(quantityInput);

   if (Number.isNaN(quantity)) {
     console.log("Quantity must be a number");
   } else {
     console.log(quantity + extraItems); // 15
   }
   ```

5. **Re-test the failure path too.** `Number("ten")` is `NaN`, and `Number.isNaN(Number("ten"))` is `true`, so bad input now produces a clear message instead of a strange total.

The tempting wrong fix is `totalItems - 0` or wrapping the final result in `Number(...)`. `Number("105")` is `105`, which is still wrong. The data was already damaged when the strings were joined, so the conversion has to happen before the arithmetic.

## Practical Guidance

- Use `const` by default.
- Use `let` when reassignment is intentional.
- Avoid `var` in modern code unless you are reading legacy code.
- Treat arrays and objects as mutable containers unless you create a copy.
- Use `===` and `!==`. Reach for `==` only if you can explain exactly what it will convert.
- Convert input strings to numbers explicitly (`Number(value)`) and check the result with `Number.isNaN`.
- Use `??` for defaults when `0`, `""`, or `false` are legitimate values.
- When a value surprises you, log it together with its type: `console.log(value, typeof value)`.

## Common Mistakes

- **Expecting assignment to copy an object.** `const b = a` shares the object. Use spread or `structuredClone` when you need a copy, and remember spread is shallow.
- **Comparing objects with `===` to check their contents.** It compares identity. Compare the fields you care about instead.
- **Doing arithmetic on strings.** `"10" + 5` is `"105"`. Convert first.
- **Using a variable before its `let` or `const` line.** That throws a `ReferenceError` (in Node the message reads `Cannot access 'later' before initialization` for a variable named `later`). Declarations are not usable until the line runs.
- **Reading a property of something that might be `null`.** Check first or use `?.`.
- **Printing raw floating-point results to users.** Format with `toFixed` or `Intl.NumberFormat`, and keep the original number for further calculations.

## Check Yourself

Predict the output, then run the code to confirm.

1. `const x = { n: 1 }; const y = x; y.n = 2; console.log(x.n);`
2. `console.log(typeof null, typeof [], Array.isArray([]));`
3. `console.log("3" * "4", "3" + "4");`
4. `const count = 0; console.log(count || 10, count ?? 10);`
5. `console.log([] ? "truthy" : "falsy");`

Answers:

1. `2`. `y` and `x` reference the same object.
2. `object object true`.
3. `12 34`. `*` converts both strings to numbers; `+` concatenates when a string is involved.
4. `10 0`. `||` treats `0` as missing; `??` does not.
5. `truthy`. Every object, including an empty array, is truthy.

## Exercises

`Lab 01A`: Create variables for a product name, price, quantity, and whether it is on sale. Log a final summary string using template literals.

- Stretch: also log the line total (`price * quantity`) formatted to two decimal places.

`Lab 01B`: Create an object called `profile`, assign it to another variable, mutate one property, and explain why both variables appear to change.

- Stretch: make a copy with spread, change the copy, and show that the original stays the same.

`Lab 01C`: Log the `typeof` result for five different values and write one sentence explaining each.

- Stretch: include `null` and an array, and explain why both say `"object"`.

See the solution guide: [Lesson 01 Solutions](../../solutions/lesson-01-solutions.md)

## References

- MDN JavaScript Guide: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide
- MDN Grammar and Types: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types
- MDN JavaScript Overview: https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript
- MDN Equality comparisons and sameness: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness
- MDN `structuredClone()`: https://developer.mozilla.org/en-US/docs/Web/API/Window/structuredClone

## Job-Readiness Takeaway

Junior engineers are constantly asked to inspect existing values, trace state changes, and understand why a variable does not contain what they expected. This lesson is simple on purpose because these core mental models are the base layer for almost every debugging task you will do later.

The shared-reference idea from this lesson comes back again and again: in React state updates (Lesson 10), in Express request handlers that modify a shared array (Lesson 07), and in tests that pass alone but fail together because they mutate the same fixture (Lesson 08). Being able to say "these two variables point at the same object" during a code review or an interview is a small, concrete signal that you understand the language rather than just its syntax.
