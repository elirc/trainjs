# Capstone Guide: Job Portfolio Full-Stack App

## Project Summary

Build a full-stack application that is realistic enough to discuss in interviews and small enough to finish. A strong default project is a `Task Tracker + Notes` app for individuals or small teams.

Core idea:

- users can create, edit, complete, and delete tasks
- each task can include notes, priority, and due dates
- the frontend displays loading, success, and error states
- the backend exposes a JSON API
- the project includes validation, tests, and a polished README

## Why This Project Works

It demonstrates:

- CRUD operations
- client/server communication
- state management
- form handling
- validation
- API design
- practical debugging
- optional TypeScript and framework integration

This is a better junior portfolio story than a purely visual clone because it shows data flow and engineering thinking.

## Milestones

### Milestone 1: Planning

- Define user stories.
- Sketch the UI.
- List entities and fields.
- Choose a simple folder structure.
- Decide whether the first version will use plain JavaScript or React for the frontend.

### Milestone 2: Frontend Foundation

- Render a task list.
- Build task creation and editing forms.
- Add validation messages.
- Show empty state and loading state.

### Milestone 3: Backend Foundation

- Create routes for listing, creating, updating, and deleting tasks.
- Validate request bodies.
- Return consistent JSON responses.
- Add an in-memory store first, then optionally move to a simple database.

### Milestone 4: Integration

- Connect the frontend to the API with `fetch`.
- Handle request errors visibly.
- Keep UI state in sync after create, update, and delete actions.

### Milestone 5: Quality

- Add tests for utility logic and validation.
- Clean up naming and file organization.
- Write a strong project README.
- Add reflection notes about tradeoffs and future improvements.

## Suggested Architecture

Frontend:

- components or UI modules
- API client helpers
- stateful page logic
- form validation helpers

Backend:

- server entry file
- routes
- validation or service helpers
- data layer abstraction

Shared:

- clear naming
- one obvious place for configuration
- one obvious way to start the app

## Example API Shape

`GET /tasks`

Returns all tasks.

`POST /tasks`

Creates a task from a JSON body such as:

```json
{
  "title": "Finish portfolio project",
  "priority": "high",
  "notes": "Add README screenshots",
  "done": false
}
```

`PATCH /tasks/:id`

Updates one or more task fields.

`DELETE /tasks/:id`

Removes a task.

## Minimum Acceptance Criteria

- The app can create, read, update, and delete tasks.
- The frontend handles loading and error states.
- The backend validates missing or invalid fields.
- The codebase is organized into understandable modules.
- At least a few meaningful tests exist.
- The README explains setup, features, tradeoffs, and future improvements.

## Common Mistakes

- building too many features before the core loop works
- skipping validation until the end
- making the UI look polished while data flow is still fragile
- writing one giant file for client or server logic
- not documenting assumptions in the README

## Interview Discussion Prompts

Prepare to answer:

- Why did you choose this project scope?
- How does data move from the UI to the API and back?
- What validation happens on the client and server?
- What bug was hardest to diagnose?
- If you had one more week, what would you improve?
- Where would TypeScript or a database add the most value?

## Stretch Improvements

- authentication
- filtering and search
- pagination
- persistent database storage
- deployment
- improved accessibility
- TypeScript across both client and server

## Final Deliverables

- source code
- screenshots or demo GIFs
- README
- test commands
- short reflection notes you can reuse in interviews
