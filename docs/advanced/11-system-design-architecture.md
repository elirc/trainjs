# Mid/Senior Prep: System Design and Architecture

## Goals

- Shift from feature-level thinking to system-level thinking.
- Understand how architecture choices affect reliability, performance, maintainability, and team velocity.
- Practice framing design tradeoffs the way stronger mid-level and senior engineers do.
- Build a practical study path for system design interviews and real-world architecture conversations.

## Prerequisites

- Comfort with the junior track in this repository or equivalent experience building small full-stack apps.
- Familiarity with APIs, databases, async work, frontend state, and debugging.

## Why This Track Exists

Getting to a junior level usually means you can implement features with guidance. Moving toward mid-level and senior work means you start owning how systems are shaped, not just how one function or screen is written.

That shift includes questions like:

- What are the most important quality attributes for this system?
- Where should the boundaries between modules, services, or teams live?
- What breaks first when usage grows?
- Which failures are acceptable, and which are business-critical?
- How do we design for change instead of only for the current feature request?

System design is not about drawing random boxes and arrows. It is structured reasoning under constraints.

## The Mental Shift

Junior-level implementation questions often sound like:

- How do I build this form?
- Why is this API call failing?
- How should I structure this component?

Mid/senior architecture questions often sound like:

- Should this capability live in the frontend, backend, or both?
- What contracts must remain stable if multiple teams depend on this service?
- Should this system be synchronous or event-driven?
- Where do we cache, and what staleness is acceptable?
- Which bottlenecks are worth solving now, and which are premature complexity?

The code still matters. Architecture is just the layer where code, constraints, and tradeoffs meet.

## Core System Design Framework

When you approach a design problem, move through it in this order.

### 1. Clarify Requirements

Separate functional and non-functional requirements.

Functional requirements define what the system does:

- users can upload images
- clients can create and update tasks
- admins can search audit logs

Non-functional requirements define what the system must be good at:

- low latency
- high availability
- strong consistency
- low cost
- easy operability
- clear compliance boundaries

Many weak designs fail because they optimize the wrong thing.

### 2. Identify Core Entities And Flows

Ask:

- What data enters the system?
- What transformations happen?
- Where is state stored?
- Which systems or users consume the result?

For a task application, the flow might be:

1. User submits a task from the UI.
2. Frontend validates basic input.
3. API validates again and writes to storage.
4. Response returns created task.
5. UI updates local state.
6. Optional notifications or analytics run asynchronously.

This simple habit prevents vague design discussions.

### 3. Find The Critical Constraints

The best design for 500 internal users is not the best design for 50 million consumers.

Ask:

- traffic volume
- peak vs steady load
- read-heavy vs write-heavy behavior
- data retention requirements
- legal or compliance needs
- team size and ownership structure
- budget and operational maturity

The more serious the constraints, the more architecture matters.

### 4. Design The Simplest Viable Architecture

Start with the simplest design that can reasonably satisfy the requirements. Do not jump to microservices because it sounds advanced.

A strong monolith with clear module boundaries is often the right first architecture. Distributed systems introduce:

- network failures
- operational overhead
- harder debugging
- eventual consistency problems
- more deployment coordination

Senior engineers are not the people who add the most components. They are often the people who know when not to.

## Architecture Building Blocks

### Clients

Clients include browsers, mobile apps, internal tools, and background workers. Think about:

- how they authenticate
- how often they request data
- how they handle slow responses
- how much logic should live on the client

### Load Balancers And Gateways

These distribute traffic and centralize concerns such as routing, TLS termination, rate limiting, and authentication checks.

Good design question:

- Do we need a gateway because of real cross-cutting concerns, or are we adding layers before they earn their keep?

### Application Servers

These contain business logic and orchestration. Key questions:

- Is the app stateless enough to scale horizontally?
- Which logic belongs here versus in background jobs?
- What should happen in the request path versus later?

### Databases

Databases are not interchangeable boxes.

Think about:

- relational vs document vs key-value patterns
- read and write shapes
- indexing strategy
- transaction needs
- reporting and analytics separation

For many product systems, a relational database is a strong default because it provides structure, constraints, and mature query support.

### Caches

Caches reduce latency and database load, but they create freshness and invalidation problems.

Ask:

- What data is read often?
- What data changes rarely?
- How stale can cached results be?
- What is the invalidation strategy?

If you cannot explain cache invalidation clearly, you probably are not ready to add that cache yet.

### Queues And Background Jobs

Move work out of the request path when it is slow, retryable, or not immediately required.

Examples:

- sending emails
- generating reports
- resizing images
- processing analytics events

This improves responsiveness, but introduces delivery guarantees and retry design questions.

## Common Architecture Styles

### Modular Monolith

A modular monolith is a single deployable application with strong internal boundaries.

Strengths:

- simpler deployment
- easier local development
- fewer network failure modes
- simpler transactions

Risks:

- boundaries can erode if the codebase lacks discipline
- large teams may step on each other
- scaling only one hotspot can be harder

Use it when:

- the product is still evolving
- the team is small to medium
- complexity is better controlled through modules than services

### Microservices

Microservices split a system into independently deployable services.

Strengths:

- clearer service ownership
- independent scaling and deployment
- strong team boundaries in larger organizations

Costs:

- much harder debugging
- network and serialization overhead
- eventual consistency
- duplicated tooling and platform concerns

Use them when:

- service boundaries are real and stable
- team ownership requires separation
- operational maturity is already strong

Most teams should earn microservices rather than start there.

### Event-Driven Architecture

In event-driven systems, components react to published events rather than direct synchronous calls.

Good fit for:

- notifications
- analytics
- asynchronous workflows
- loose coupling between producers and consumers

Risks:

- harder traceability
- harder local reasoning
- eventual consistency
- schema evolution problems

### Layered Frontend Architecture

Frontend architecture matters too. A mature frontend is not just components everywhere.

Healthy boundaries often separate:

- UI components
- stateful page logic
- API client layer
- validation helpers
- domain formatting utilities

When mid-level frontend engineers grow, this is one of the first architecture skills they develop.

## Example Evolution: From Junior App To Production-Conscious System

Imagine the task tracker from the junior capstone.

### Version 1

- single frontend
- single backend app
- one database
- direct request/response flow

This is good. Do not apologize for it.

### Version 2

Usage grows and product needs expand:

- users want reminders
- managers want reporting
- the app feels slow during peaks
- task search gets expensive

At this stage, you might add:

- database indexes for common queries
- caching for expensive reads
- background jobs for reminders and reporting
- pagination for large task lists
- more explicit module boundaries

### Version 3

Only if the domain and team demand it, you might consider:

- separating notifications into its own service
- separating analytics pipelines from the transactional system
- introducing event-driven flows for non-critical side effects

Notice the pattern: architecture should follow pressure, not ego.

## Reliability And Failure Thinking

Mid-level and senior engineers are expected to think about failure modes before production does it for them.

Ask:

- What happens if the database is slow?
- What happens if the downstream service times out?
- What happens if a retry causes duplicate effects?
- What happens if a worker processes the same message twice?
- What happens if one region or instance disappears?

Useful patterns:

- timeouts
- retries with limits
- idempotency
- circuit breakers
- health checks
- graceful degradation

You do not need every resilience pattern everywhere. You do need to know which failures matter most.

## Data Design And Consistency

A lot of architecture is really data design wearing a different outfit.

Think about:

- source of truth
- ownership of each entity
- write paths
- consistency requirements
- auditability
- retention

Questions to practice:

- Does this operation require strong consistency, or is eventual consistency acceptable?
- Should we normalize this data, denormalize it, or maintain both forms?
- Which writes must be transactional?
- How will schema changes be introduced safely?

Senior engineers are often good because they can see data risks early.

## Performance Thinking

Performance work starts with measurement, not guessing.

Look for:

- slow queries
- repeated requests
- oversized payloads
- unnecessary re-renders
- serialized work that could be parallelized
- CPU-heavy tasks in the request path

Useful performance levers:

- indexing
- caching
- batching
- pagination
- compression
- CDN use
- background processing

The best performance improvement is often removing avoidable work.

## Observability And Operations

Architecture is incomplete if the team cannot understand the system in production.

You need:

- logs for events and failures
- metrics for throughput, latency, error rate, and resource usage
- tracing for cross-service request paths
- dashboards for ongoing health
- alerts tied to user or business impact

A system you cannot observe is a system you cannot safely evolve.

## Security As An Architecture Concern

Security is not only a checklist after the build is done.

Architecture-level security questions include:

- Where does authentication happen?
- Where does authorization happen?
- Which data is sensitive?
- What should be encrypted in transit and at rest?
- What is the blast radius if one token or service is compromised?

Do not treat security as a separate discipline you can ignore until you become senior. The stronger habit is to treat it as a design dimension from the start.

## Team And Codebase Architecture

System architecture and team architecture influence each other.

Signs of healthy architecture:

- ownership is clear
- module boundaries are understandable
- interfaces are stable enough for collaboration
- local development is still possible
- teams can change one area without breaking unrelated ones

This is why architecture is not only about scale. It is also about change management.

## Refactoring Toward Better Architecture

Most architecture work is not greenfield system design. It is improving an existing system carefully.

Good refactoring strategy:

1. Identify the real pain.
2. Measure where possible.
3. Improve boundaries before splitting deployments.
4. Migrate incrementally.
5. Preserve behavior while changing structure.
6. Document the new model clearly.

Common mistake:

- redesigning everything at once instead of targeting the constraint that actually hurts

## How To Practice System Design

Do not wait for an interview to start practicing.

Use this routine:

1. Pick a familiar product or feature.
2. Write its functional and non-functional requirements.
3. Sketch the simplest viable architecture.
4. Identify bottlenecks and failure modes.
5. Propose one or two incremental improvements.
6. Explain the tradeoffs in plain English.

Good practice prompts:

- Design a task management app for 500 internal users.
- Design a notification system for reminders and alerts.
- Design an activity feed with high read traffic.
- Design file upload and image processing for a portfolio app.
- Design a metrics dashboard that refreshes every few seconds.

## Interview Framework

In system design interviews, strong candidates usually do not jump straight into details. They:

1. clarify scope
2. identify priorities
3. propose a simple baseline
4. walk through data flow
5. discuss scaling and failure points
6. explain tradeoffs calmly

What interviewers often want to hear:

- explicit assumptions
- awareness of tradeoffs
- practical defaults
- sensible boundaries
- maturity about operational concerns

What hurts candidates:

- overengineering immediately
- vague buzzwords without data flow
- forgetting failure modes
- ignoring non-functional requirements

## Training Roadmap

### Stage 1: Foundation

- master the junior track in this repo
- build and ship the capstone
- read more production code

### Stage 2: Structured Architecture Thinking

- practice 1 small design prompt per week
- document requirements, bottlenecks, and tradeoffs
- compare a modular monolith design with a distributed alternative

### Stage 3: Production-Conscious Growth

- study reliability, caching, data modeling, and observability
- look at how real teams handle incidents and migrations
- review architecture decision records if your team uses them

### Stage 4: Senior-Oriented Communication

- present designs clearly in docs and diagrams
- justify tradeoffs without overclaiming certainty
- lead conversations around scope, failure, and change cost

## Exercises

`Exercise 11A`: Take the junior capstone and redesign it for 50,000 daily active users. Write down which parts of the original design break first and what you would change in what order.

`Exercise 11B`: Compare a modular monolith and a microservice version of the same task platform. Explain why the monolith may still be the better choice.

`Exercise 11C`: Design a notification subsystem for email and in-app reminders. Decide which parts must be synchronous and which should be asynchronous.

`Exercise 11D`: Pick one slow page in a hypothetical app and list five possible performance bottlenecks from browser to database.

`Exercise 11E`: Write a one-page design note with these headings: problem, requirements, baseline design, bottlenecks, tradeoffs, and next steps.

## References

- MDN HTTP Caching: https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching
- AWS Well-Architected Framework: https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
- Google Cloud Well-Architected Framework: https://cloud.google.com/architecture/framework
- Martin Fowler Microservices Guide: https://www.martinfowler.com/microservices/

## Career Takeaway

The move from junior to mid-level and senior is not mainly about memorizing more APIs. It is about seeing software as a living system with users, data flows, operational risk, and change cost.

If the junior track teaches you how to build, this advanced track teaches you how to reason about what should be built, where complexity belongs, and how systems stay healthy as they grow.
