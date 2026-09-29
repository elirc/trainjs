# Lesson 05: Async JavaScript, Promises, Fetch, APIs, and UI Flows

## Goals

- Understand why asynchronous code exists.
- Use promises and `async/await` confidently.
- Fetch data from APIs and handle loading, success, and failure states.
- Avoid common mistakes around timing and error handling.

## Prerequisites

- Lessons 01-04.

## Concepts

JavaScript often waits for things: network requests, timers, user input, file reads. Instead of blocking everything, JavaScript schedules follow-up work. Promises represent values that may be available later.

`async/await` improves readability, but it does not replace the need to understand promise flow. `await` pauses only inside the current async function, not the entire program.

## Worked Example

```js
async function loadPosts() {
  const status = document.querySelector("#status");
  const list = document.querySelector("#posts");

  status.textContent = "Loading...";

  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts?_limit=3");

    if (!response.ok) {
      throw new Error(`Request failed with status ${response.status}`);
    }

    const posts = await response.json();

    list.innerHTML = posts
      .map(post => `<li>${post.title}</li>`)
      .join("");

    status.textContent = "Loaded.";
  } catch (error) {
    status.textContent = `Error: ${error.message}`;
  }
}
```

## Explaining The Code

This function handles the full UI flow:

- show loading state
- send request
- check HTTP status
- parse JSON
- render result
- show a clear error message if anything goes wrong

A common beginner mistake is assuming `fetch` throws on every failed HTTP status. It does not. `fetch` only rejects for network-level failures. A `404` or `500` still resolves, so you must check `response.ok`.

## Promise Example

```js
function wait(ms) {
  return new Promise(resolve => {
    setTimeout(resolve, ms);
  });
}

wait(1000).then(() => console.log("One second passed"));
```

This is the promise version of a delay. Understanding simple custom promises makes other async patterns less mysterious.

## Exercises

`Lab 05A`: Fetch a list of users from a public API and render names into the page.

`Lab 05B`: Add loading and error messages.

`Lab 05C`: Write a `delay(ms)` helper that returns a promise and use it inside an async function.

See the solution guide: [Lesson 05 Solutions](../../solutions/lesson-05-solutions.md)

## References

- MDN Promises: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises
- MDN Fetch API: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
- Node.js Fetch Guide: https://nodejs.org/en/learn/getting-started/fetch

## Job-Readiness Takeaway

Most modern JavaScript jobs involve async behavior all day long. Data fetching, loading spinners, retries, form submission, and state synchronization all depend on these ideas. If you can model async flow clearly, you become much easier to trust on real app work.
