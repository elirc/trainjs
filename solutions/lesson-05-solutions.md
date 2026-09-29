# Lesson 05 Solutions

## Lab 05A

```js
async function loadUsers() {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");

  if (!response.ok) {
    throw new Error(`Status: ${response.status}`);
  }

  const users = await response.json();
  const list = document.querySelector("#users");

  list.innerHTML = users.map(user => `<li>${user.name}</li>`).join("");
}
```

## Lab 05B

```js
async function showUsers() {
  const status = document.querySelector("#status");

  status.textContent = "Loading...";

  try {
    await loadUsers();
    status.textContent = "Loaded users.";
  } catch (error) {
    status.textContent = `Error: ${error.message}`;
  }
}
```

## Lab 05C

```js
function delay(ms) {
  return new Promise(resolve => {
    setTimeout(resolve, ms);
  });
}
```
