# Lesson 01 Solutions

Try each lab before reading its solution. Each code block below can be saved as an `.mjs` file and run with `node`; the outputs shown are what it should print. Your values and wording can differ. What matters is that you can explain why your output looks the way it does.

Back to the lesson: [Lesson 01: JavaScript Foundations and Mental Models](../docs/lessons/01-javascript-foundations.md)

## Lab 01A

```js
const productName = "Mechanical Keyboard";
const price = 79.99;
const quantity = 2;
const onSale = true;

const summary = `${productName}: ${quantity} items at $${price} each. On sale: ${onSale}`;
console.log(summary);
```

Output:

```text
Mechanical Keyboard: 2 items at $79.99 each. On sale: true
```

Each `${ }` evaluates an expression and turns the result into text. `$${price}` is a literal `$` followed by the embedded `price`. The boolean `true` is printed as the word `true`.

Stretch (line total and a friendlier sale label):

```js
const lineTotal = price * quantity;
console.log(lineTotal);
console.log(`Line total: $${lineTotal.toFixed(2)}`);
console.log(`Status: ${onSale ? "On sale" : "Full price"}`);
```

Output:

```text
159.98
Line total: $159.98
Status: On sale
```

Here `79.99 * 2` happens to print cleanly, but do not rely on that: as the lesson showed, `19.99 + 19.99 * 0.08` prints `21.589199999999998` (and so does `19.99 * 1.08`). Always format money with `toFixed(2)` (or `Intl.NumberFormat`) when you display it.

Common wrong answers:

- Using normal quotes, `"${productName}"`. Only backtick strings interpolate; in double quotes you get the literal characters `${productName}`.
- Storing the price as a string (`"79.99"`) and then multiplying or adding. Multiplication would still convert it, but `"79.99" + 1` would give `"79.991"`.

## Lab 01B

```js
const profile = { name: "Jordan", track: "JavaScript" };
const sameProfile = profile;

sameProfile.track = "Full-Stack JavaScript";

console.log(profile.track);
console.log(sameProfile.track);
console.log(profile === sameProfile);
```

Output:

```text
Full-Stack JavaScript
Full-Stack JavaScript
true
```

Both variables reference the same object. There is only one object in memory; `profile` and `sameProfile` are two labels pointing at it. `profile === sameProfile` is `true` because `===` on objects checks identity.

Stretch (a real copy):

```js
const copy = { ...profile };
copy.track = "Frontend";
console.log(profile.track, copy.track, profile === copy);
```

Output:

```text
Full-Stack JavaScript Frontend false
```

The spread creates a new object, so changing `copy.track` leaves `profile` alone. This copy is shallow. If `profile` had a nested object (for example `profile.address`), both objects would still share that nested object.

Common wrong answers:

- "Because `const` makes them linked." `const` has nothing to do with it; `let` behaves the same way. The link is the shared reference.
- "JavaScript copies objects lazily." It does not copy them at all on assignment.

## Lab 01C

The lab asks for `typeof` on string, number, boolean, object, and undefined values. This version includes a few extras:

```js
const samples = ["Jordan", 42, true, { name: "Jordan" }, undefined, null, [1, 2], () => {}];

for (const value of samples) {
  console.log(typeof value);
}
```

Output:

```text
string
number
boolean
object
undefined
object
object
function
```

One sentence each:

- `"Jordan"` is a string primitive.
- `42` is a number primitive; JavaScript has one `number` type for integers and decimals.
- `true` is a boolean primitive.
- `{ name: "Jordan" }` is an object, a reference value.
- `undefined` is its own primitive type and means "no value has been given".
- `null` reports `"object"` because of a long-standing bug in the language; it is actually a primitive meaning "intentionally empty".
- `[1, 2]` reports `"object"` because arrays are objects; use `Array.isArray` to tell them apart.
- `() => {}` reports `"function"`; functions are objects too, but `typeof` gives them their own label.

The important takeaway is not memorizing every output mechanically. It is recognizing which values are primitive and which are reference-based.

Common wrong answer: expecting `typeof []` to be `"array"`. There is no such `typeof` result.
