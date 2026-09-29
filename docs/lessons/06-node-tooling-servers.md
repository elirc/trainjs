# Lesson 06: Node.js Fundamentals, Packages, Tooling, and Server Basics

## Goals

- Understand what Node.js is and what it is not.
- Use npm packages and scripts productively.
- Read environment-based code with more confidence.
- Build a minimal HTTP server and understand the request/response cycle.

## Prerequisites

- Lessons 01-05.

## Concepts

Node.js lets JavaScript run outside the browser. It provides runtime APIs for files, processes, modules, networking, and more. The language is still JavaScript, but the environment is different.

As a junior developer, you do not need to master every Node core module immediately. You do need to understand the role of:

- `package.json`
- dependencies vs devDependencies
- npm scripts
- environment variables
- server entry files

## Worked Example

```js
import http from "node:http";

const server = http.createServer((request, response) => {
  response.writeHead(200, { "Content-Type": "application/json" });
  response.end(JSON.stringify({ message: "Server is running" }));
});

server.listen(3000, () => {
  console.log("Listening on http://localhost:3000");
});
```

## Explaining The Code

This server listens for incoming requests on port `3000`. When a request arrives, it sends a JSON response with an HTTP status code and headers. Even if you later use Express or another framework, this low-level model stays important:

- the client sends a request
- the server reads it
- your code decides what response to send

## npm Script Example

```json
{
  "scripts": {
    "dev": "node server.js",
    "test": "node --test"
  }
}
```

Scripts standardize project tasks. Teams rely on this because it reduces "works on my machine" confusion.

## Exercises

`Lab 06A`: Create a `package.json` with a `dev` script and explain what it does.

`Lab 06B`: Build a small HTTP server that returns plain text on `/` and JSON on `/health`.

`Lab 06C`: Add one environment variable, such as a port number, and use it in your server.

See the solution guide: [Lesson 06 Solutions](../../solutions/lesson-06-solutions.md)

## References

- Node.js Learn: https://nodejs.org/en/learn
- Node.js Docs Overview: https://nodejs.org/api/documentation.html
- MDN HTTP Overview: https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview

## Job-Readiness Takeaway

Many junior full-stack roles expect you to read backend code even when you are not the main backend owner. Understanding the server lifecycle, scripts, and environment config makes you far more useful on mixed frontend/backend teams.
