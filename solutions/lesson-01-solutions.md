# Lesson 01 Solutions

## Lab 01A

```js
const productName = "Mechanical Keyboard";
const price = 79.99;
const quantity = 2;
const onSale = true;

const summary = `${productName}: ${quantity} items at $${price} each. On sale: ${onSale}`;
console.log(summary);
```

## Lab 01B

```js
const profile = { name: "Jordan", track: "JavaScript" };
const sameProfile = profile;

sameProfile.track = "Full-Stack JavaScript";

console.log(profile.track);
console.log(sameProfile.track);
```

Both variables reference the same object.

## Lab 01C

Use `typeof` on string, number, boolean, object, and undefined values. The important takeaway is not memorizing every output mechanically. It is recognizing which values are primitive and which are reference-based.
