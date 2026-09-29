# Lesson 10 Solutions

## Lab 10A

```jsx
function UserList({ users }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

## Lab 10B

Imperative DOM updates tell the browser step by step what to change. Declarative rendering describes the UI for the current state and lets the framework handle the update process.

## Lab 10C

Strong JavaScript fundamentals for React include functions, array methods, object updates, events, modules, and async thinking.
