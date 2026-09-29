# Course Overview

## Summary

This course teaches JavaScript as a working language, not a trivia topic. The main idea is simple: junior developers become effective when they can reason about values, functions, state, asynchronous behavior, and program structure with confidence. Everything in this course points back to that.

The main path in this repository is a junior job-readiness track. After that, the docs extend into an advanced track focused on system design and architecture for mid-level and senior growth.

## Learning Strategy

The curriculum moves in a deliberate order:

1. Learn how JavaScript thinks about values and execution.
2. Learn how to structure logic using functions, scope, and data.
3. Learn how larger programs organize behavior with objects and modules.
4. Learn how JavaScript interacts with browsers and servers.
5. Learn how real apps handle async work, APIs, validation, and failures.
6. Learn how teams use tooling, tests, TypeScript, and frameworks without losing the core language.

## What "Job Ready" Means Here

Job ready does not mean expert. It means you can:

- take a small task ticket and break it down
- read existing JavaScript without freezing
- add features with reasonable structure
- ask good questions when blocked
- test and debug your work
- explain tradeoffs clearly enough for code review and interviews

## Study Workflow

Use the same workflow for every lesson:

1. Read the goals and prerequisites.
2. Work through examples slowly.
3. Re-type the code and change one thing at a time.
4. Write down predictions before running code.
5. Complete the lab without looking at solutions.
6. Compare your code to the solution and note what you missed.
7. Summarize the lesson in plain English.

## Required Habits

- Keep a running `questions.md` file for topics that still feel fuzzy.
- Commit small checkpoints if you place exercises into a practice repo.
- Say out loud what each function receives, returns, and mutates.
- When using AI, ask for explanation and critique rather than just answers.

## Common Beginner Traps

- thinking `this` and scope are the same thing
- confusing copying a reference with copying a value
- using `async/await` without understanding promises
- treating `fetch` errors and HTTP errors as the same
- writing code that works once but is hard to change
- jumping to frameworks before understanding the language

## Deliverables

By the time you finish, you should produce:

- completed lesson labs
- a set of notes or code snippets you understand well
- a full-stack capstone with README, features, and reflection notes
- a short list of stories you can tell in an interview about bugs, tradeoffs, and learning

## Progress Markers

You are on track if:

- by Lesson 3, you can explain scope and closures clearly
- by Lesson 5, you can fetch data and render loading/error states
- by Lesson 7, you can build and consume a small API
- by Lesson 9, TypeScript feels helpful rather than magical
- by the capstone, you can work across client, server, and data flow

## After The Junior Track

Once the core course feels comfortable, the next growth step is not memorizing more syntax. It is learning to think in systems.

That means being able to answer questions like:

- What are the critical parts of this system?
- Where should the boundaries between modules or services be?
- What happens when traffic increases or dependencies fail?
- Which tradeoffs are we making around consistency, speed, cost, and complexity?
- How do we keep the system understandable for the next team that inherits it?

The advanced guide in this repository is intended to train that next layer of thinking:

- [Mid/Senior Prep: System Design and Architecture](advanced/11-system-design-architecture.md)

You do not need to wait until you have a senior title to start learning architecture. You do need enough implementation experience to connect the higher-level ideas back to real code and real product constraints.

## Alternate Learning Style Track

Not everyone learns best from long concept-first lessons. Some learners understand faster when they see a very small snippet, predict the behavior, and then read a careful breakdown of what happened.

That is why this repository also includes an example-driven JavaScript and React training guide:

- [Example-Driven JavaScript and React Training](supplemental/12-example-driven-js-react-training.md)
- [Example-Driven JavaScript Fundamentals Drills](supplemental/13-example-driven-js-fundamentals-drills.md)

Use it when:

- the main lessons feel too abstract
- you want extra repetition without re-reading whole modules
- you learn best by tracing short examples line by line
- you want more React-oriented reinforcement after the core JavaScript track

## Interview Review Track

Some interview practice is less about solving a problem on the spot and more about explaining common concepts clearly and quickly.

That is why this repository also includes trivia-style review sheets:

- [JavaScript Language Trivia Review](interview/14-javascript-language-trivia-review.md)
- [React and Browser Trivia Review](interview/15-react-browser-trivia-review.md)
- [Runtime, TypeScript, and Tooling Trivia Review](interview/16-runtime-typescript-tooling-trivia-review.md)

Use them when:

- you want fast self-quiz review
- you need sharper recall for language features and definitions
- you want to practice concise interview answers without writing code
