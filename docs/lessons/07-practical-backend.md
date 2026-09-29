# Lesson 07: Practical Backend Development and Integration

## Goals

- Build a small REST-style API.
- Understand routing, middleware, validation, and persistence at a junior practical level.
- Connect frontend and backend thinking into one system.

## Prerequisites

- Lessons 01-06.

## Concepts

Backend code exists to receive requests, apply business rules, read or write data, and return responses. For junior-level work, focus on clarity before cleverness.

An Express-style app usually contains:

- app setup
- middleware
- route handlers
- validation logic
- data access layer or temporary in-memory store

## Worked Example

```js
import express from "express";

const app = express();
app.use(express.json());

const tasks = [];

app.get("/tasks", (req, res) => {
  res.json(tasks);
});

app.post("/tasks", (req, res) => {
  const { title } = req.body;

  if (!title || title.trim() === "") {
    return res.status(400).json({ error: "Title is required" });
  }

  const task = {
    id: Date.now(),
    title: title.trim(),
    done: false
  };

  tasks.push(task);
  res.status(201).json(task);
});
```

## Explaining The Code

`express.json()` parses JSON request bodies so `req.body` is usable. The `POST /tasks` route validates input before creating a task. This sequence matters:

1. parse request
2. validate input
3. apply logic
4. store data
5. return a response

Skipping validation is one of the fastest ways to create bugs and security problems.

## Persistence Concepts

At first, an in-memory array is enough to learn flow. Then you should understand why it is limited:

- data disappears when the server restarts
- it does not scale across multiple instances
- it makes queries and relationships harder

That is where databases enter the picture. For junior readiness, you need the concept and the integration pattern more than deep database administration.

## Exercises

`Lab 07A`: Add a `DELETE /tasks/:id` route.

`Lab 07B`: Add a `PATCH /tasks/:id` route that toggles `done`.

`Lab 07C`: Write a short paragraph explaining when an in-memory array stops being enough.

See the solution guide: [Lesson 07 Solutions](../../solutions/lesson-07-solutions.md)

## References

- Express Basic Routing: https://expressjs.com/en/starter/basic-routing.html
- Express Routing Guide: https://expressjs.com/en/guide/routing.html
- MDN HTTP Status: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

## Job-Readiness Takeaway

This lesson is close to real junior backend work. You are translating input into validated behavior and predictable responses. That is the heart of many internal tools, CRUD apps, and small production services.
