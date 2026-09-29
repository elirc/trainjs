# Lesson 06 Solutions

## Lab 06A

```json
{
  "scripts": {
    "dev": "node server.js"
  }
}
```

The script gives the team one standard command for starting the app.

## Lab 06B

```js
import http from "node:http";

const server = http.createServer((request, response) => {
  if (request.url === "/") {
    response.writeHead(200, { "Content-Type": "text/plain" });
    response.end("Hello from the server");
    return;
  }

  if (request.url === "/health") {
    response.writeHead(200, { "Content-Type": "application/json" });
    response.end(JSON.stringify({ ok: true }));
    return;
  }

  response.writeHead(404, { "Content-Type": "text/plain" });
  response.end("Not found");
});
```

## Lab 06C

```js
const port = process.env.PORT || 3000;
server.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
```
