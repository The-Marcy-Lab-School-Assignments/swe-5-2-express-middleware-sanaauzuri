# Short Response Questions

Answer each question below in your own words. Aim for 3–5 sentences per answer. Be specific — use the exact terms and concepts from the lesson.

Your responses will each be evaluated out of 6 points. You can earn 3 points for writing quality and 3 points for the accuracy and precision of the technical content per question.

---

## Question 1: Express vs `node:http`

Express is described as a framework that "wraps" `node:http`. What does that mean? Compare how you would handle a `GET /api/users` request in `node:http` versus in Express. What does Express do for you automatically that you had to write manually with `node:http`?

**Your answer here**:

Express is described as a framework that "wraps" `node:http` because Express encases the repetitive code/work of `node:http` into one or two lines of code. With node:http, handling a `GET /api/users` request means writing if/else chains on `req.method` and `req.url`, manually calling `res.writeHead()` to set headers on each response, `JSON.stringify()` to convert data on each response body, and `res.end()` to send the response on every code path. With Express, you could just write `app.get('/api/users', serveUsers)` and use `res.send(users)`. That one line automatically sets the status to 200, sets the `Content-Type` header to `application/json`, and serializes the object to JSON.


## Question 2: Endpoints, Controllers, and Middleware

What are **controllers** and **middleware** in Express? What are each responsible for and how do they work together to handle incoming requests?

**Your answer here**:

A **controller** is a `callback function` tied to a specific request that reads the `req` object and sends back a response using `res`. **Middleware** is similar to a controller, but instead of sending a response, it logs the request and then calls `next()` to pass the request along to a controller to send a response. Middleware runs first for every incoming request, then the right controller takes over and sends the final response.


## Question 3: Query Strings and Route Parameters

How are **query strings** and **route parameters** similar? How are they different? In your answer, provide an example of when you would use each.

**Your answer here**:

Both **query strings** and **route parameters** are properties of the `req` object and allow the client to filter or request certain data from the server. The difference is how they appear in the `URL`. **Query strings** come after a ? as `key=value` pairs. For example, `/api/users?contains=a` is a query string and is used to filter through user data to find users that contain the letter A. **Route parameters** are named segments directly in the `URL` path, like `/api/users/:id`, and could be used to target one specific resource **(user)** by a unique identifier **(userId)**.


## Question 4: Same-Origin Requests

For API fetch calls from a client-side application, explain the difference between fetching from endpoints with relative paths like `/api/quotes` and fetching from endpoints with a full URL like `https://dog.ceo/api/breeds/image/random`. Why do we not send a fetch using a url like `http://localhost:8080/api/quotes`?

**Your answer here**:

When we fetch from a full URL like `https://dog.ceo/api/breeds/image/random`, it's a **cross-origin** request because the origin of the request, or client and the server are different. But when our client is using the same Express server as our API, both at `http://localhost:8080`, we can use a relative path like `/api/quotes` because the browser assumes it's a **same origin** request. We avoid writing `http://localhost:8080/api/quotes` because `localhost` exists on only our machine, and once the app is deployed that hardcoded URL would break.