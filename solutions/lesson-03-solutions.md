# Lesson 03 Solutions

## Lab 03A

```js
class BankAccount {
  constructor() {
    this.balance = 0;
  }

  deposit(amount) {
    this.balance += amount;
  }

  withdraw(amount) {
    this.balance -= amount;
  }

  getBalance() {
    return this.balance;
  }
}
```

## Lab 03B

Use one file to export a helper and another to import it. The key idea is clear boundaries, not file count.

## Lab 03C

```js
function safeParse(json, fallback = null) {
  try {
    return JSON.parse(json);
  } catch {
    return fallback;
  }
}
```
