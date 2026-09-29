# Lesson 02 Solutions

## Lab 02A

```js
function getGrade(score) {
  if (score >= 90) return "A";
  if (score >= 80) return "B";
  if (score >= 70) return "C";
  if (score >= 60) return "D";
  return "F";
}
```

## Lab 02B

```js
function makeGreeter(name) {
  return function greet() {
    return `Hello, ${name}!`;
  };
}
```

## Lab 02C

```js
const inStock = products.filter(product => product.inStock);
```

## Lab 02D

A returned value comes back to the caller directly. Mutation changes something outside the function, which can make the function harder to reason about and test.
