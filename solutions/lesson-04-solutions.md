# Lesson 04 Solutions

## Lab 04A

```js
const form = document.querySelector("#todo-form");
const input = document.querySelector("#todo-input");
const list = document.querySelector("#todo-list");

form.addEventListener("submit", event => {
  event.preventDefault();

  const value = input.value.trim();
  if (!value) return;

  const item = document.createElement("li");
  item.textContent = value;
  list.append(item);

  input.value = "";
});
```

## Lab 04B

```js
const tasks = [];

function saveTasks() {
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function loadTasks() {
  const raw = localStorage.getItem("tasks");
  return raw ? JSON.parse(raw) : [];
}
```

## Lab 04C

```js
const message = document.querySelector("#message");

if (input.value.trim() === "") {
  message.textContent = "Task text is required.";
  return;
}
```
