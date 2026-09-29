# Lesson 04: DOM, Browser APIs, Events, Forms, Storage, and Debugging

## Goals

- Manipulate the DOM with clear intent.
- Use events to respond to user behavior.
- Read and validate form input.
- Store small amounts of data in the browser.
- Use developer tools to debug browser code.

## Prerequisites

- Lessons 01-03.

## Concepts

In browser JavaScript, the page is represented as a tree of nodes called the Document Object Model. JavaScript does not "draw pixels directly" in most app code. It usually reads state, changes the DOM, and reacts to events.

Browser APIs are environment features provided by the browser, not by the language itself. Examples include `document`, `window`, `localStorage`, timers, and network APIs.

## Worked Example

```html
<form id="signup-form">
  <input id="email" type="email" />
  <button type="submit">Join</button>
</form>
<p id="message"></p>
```

```js
const form = document.querySelector("#signup-form");
const emailInput = document.querySelector("#email");
const message = document.querySelector("#message");

form.addEventListener("submit", event => {
  event.preventDefault();

  const email = emailInput.value.trim();

  if (!email.includes("@")) {
    message.textContent = "Please enter a valid email.";
    return;
  }

  localStorage.setItem("savedEmail", email);
  message.textContent = `Saved ${email}`;
});
```

## Explaining The Code

The `submit` event would normally refresh the page. `event.preventDefault()` stops that default behavior so your JavaScript can validate and respond first. The code then reads input, validates it, stores it, and updates the DOM.

## Debugging Workflow

When something breaks in the browser:

1. Open DevTools.
2. Inspect the console for errors.
3. Confirm your selector actually found an element.
4. Log the values you think are present.
5. Use breakpoints when the problem depends on timing or event order.

## Common Mistakes

- querying the DOM before the elements exist
- attaching listeners to the wrong node
- forgetting `preventDefault()` on forms
- storing complex data in `localStorage` without `JSON.stringify`

## Exercises

`Lab 04A`: Build a to-do form that adds list items to the page.

`Lab 04B`: Save the to-do list to `localStorage` and reload it on page load.

`Lab 04C`: Add simple validation so blank items are rejected with a visible message.

See the solution guide: [Lesson 04 Solutions](../../solutions/lesson-04-solutions.md)

## References

- MDN DOM Introduction: https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction
- MDN EventTarget `addEventListener`: https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener
- MDN Web Storage API: https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API

## Job-Readiness Takeaway

Junior frontend work often looks exactly like this lesson: collect input, validate it, update the page, persist some state, and debug why the UI is not responding. The more comfortable you get here, the more approachable frameworks will feel later.
