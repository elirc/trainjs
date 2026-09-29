# Lesson 07 Solutions

## Lab 07A

```js
app.delete("/tasks/:id", (req, res) => {
  const id = Number(req.params.id);
  const index = tasks.findIndex(task => task.id === id);

  if (index === -1) {
    return res.status(404).json({ error: "Task not found" });
  }

  tasks.splice(index, 1);
  res.status(204).end();
});
```

## Lab 07B

```js
app.patch("/tasks/:id", (req, res) => {
  const id = Number(req.params.id);
  const task = tasks.find(item => item.id === id);

  if (!task) {
    return res.status(404).json({ error: "Task not found" });
  }

  task.done = typeof req.body.done === "boolean" ? req.body.done : !task.done;
  res.json(task);
});
```

## Lab 07C

An in-memory array stops being enough when you need persistence across restarts, more reliable querying, or support for more than one running server instance.
