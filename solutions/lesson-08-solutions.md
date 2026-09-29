# Lesson 08 Solutions

## Lab 08A

```js
import { strict as assert } from "node:assert";
import test from "node:test";

function calculateTotal(items) {
  return items.reduce((sum, item) => sum + item.price, 0);
}

test("returns 0 for an empty array", () => {
  assert.equal(calculateTotal([]), 0);
});

test("adds normal prices", () => {
  assert.equal(calculateTotal([{ price: 5 }, { price: 10 }]), 15);
});

test("handles decimal prices", () => {
  assert.equal(calculateTotal([{ price: 1.5 }, { price: 2.5 }]), 4);
});
```

## Lab 08B

```js
function isValidTitle(title) {
  return typeof title === "string" && title.trim().length > 0;
}
```

Test one valid input and at least two invalid inputs such as `""` and `undefined`.

## Lab 08C

A good answer names the bug, expected behavior, reproduction steps, the layer being inspected, and how the final fix was confirmed.
