#   Express.js

- **Express.js** is a minimal and flexible Node.js web framework.
- It simplifies backend development by offering built-in routing, middleware support, and easy request/response handling.

## Setting up basic server
```
const express = require('express');
const app = express(); //initialize app
const PORT = process.env.PORT || 3000; //after including .env

app.get('/', (req, res) => {
  res.send('Hello Express!');
});

app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```
## Understanding `req.body` and `req.query`

 1. `req.body` – Request Body

 What it is:
- Holds data sent in **POST, PUT, PATCH** requests.
- Common for sending **form data**, **JSON**, or **files**.

Example:
POST /login
Body:
{
"username": "lahari",
"password": "123456"
}
How to Access:
```js
app.use(express.json());
app.post('/login', (req, res) => {
  const { username, password } = req.body;
});
```
#### use express.json() or express.urlencoded() middleware to parse the body.

2. req.query – URL Query Parameters
   
Holds key-value pairs in the URL after a question mark (?).

Used mostly in GET requests for filtering, pagination, searching.

 Example:

GET /search?name=lahari&age=20
How to Access:
app.get('/search', (req, res) => {
  const name = req.query.name;
  const age = req.query.age;
});

#### No need of any middleware

### What are Route Parameters?
Route parameters are like blanks in the URL that you can fill with real values when sending a request.
```
app.get('/user/:id', (req, res) => {
  console.log(req.params.id); // shows the id from the URL
  res.send("User ID is " + req.params.id);
});
If you visit:
http://localhost:3000/user/123
The output will be:
User ID is 123
```
Why use this?<br>
You want to show details of a specific user, product, or anything dynamic.

Example: /blog/:postId, /product/:productId



| Feature         | `req.params`                 | `req.query`                    | `req.body`                 |
|-----------------|------------------------------|--------------------------------|----------------------------|
| Comes from      | URL path (`/user/:id`)       | URL after `?` (`?key=value`)   | Request body (JSON/form)   |
| Used in         | Mostly GET, dynamic routes, used for resource identification  | GET for filtering, sorting,searching     | POST/PUT to send data (to access we shld use middleware)      |
| Format          | Path string                  | Key-value in URL               | JSON or form data          |
| Accessed using  | `req.params.key`             | `req.query.key`                | `req.body.key`             |


 ## What is a Route?

A **route** in Express is a way to handle HTTP requests to specific **URLs**.  
Each route matches a request **method** (GET, POST, etc.) and a **path**, then runs a function to respond.

#### Route handlers with req and res

 req (Request Object)<br>
Carries info from the client:<br>
req.body → Data from form/JSON<br>
req.query → Data from URL query ?<br>
req.params → Data from URL path :id<br>


res (Response Object)<br>
Used to send back a response:<br>
res.send() → Send string or object<br>
res.json() → Send JSON<br>
res.status() → Set status code<br>

## HTTP Status Codes

Status Code Categories

| Range   | Type                      | Meaning                          |
|---------|---------------------------|----------------------------------|
| 1xx     | Informational             | Request received, continuing     |
| 2xx     | Success                   | Request was successful           |
| 3xx     | Redirection               | Further action needed            |
| 4xx     | Client Error              | Client made a bad request        |
| 5xx     | Server Error              | Server failed to fulfill request |


2xx – Success Responses

| Code | Meaning              | When to Use                           |
|------|----------------------|----------------------------------------|
| 200  | OK                   | Request succeeded                     |
| 201  | Created              | New resource created (POST success)   |
| 204  | No Content           | Success but no content in response    |


4xx – Client Error Responses

| Code | Meaning                | When to Use                            |
|------|------------------------|----------------------------------------|
| 400  | Bad Request            | Invalid data (e.g., missing fields)    |
| 401  | Unauthorized           | Auth required (e.g., login needed)     |
| 403  | Forbidden              | Authenticated but no permission        |
| 404  | Not Found              | Route or resource does not exist       |
| 409  | Conflict               | Duplicate entry, already exists        |


5xx – Server Error Responses

| Code | Meaning              | When to Use                            |
|------|----------------------|----------------------------------------|
| 500  | Internal Server Error| Something broke in the backend         |
| 502  | Bad Gateway          | Server received an invalid response    |
| 503  | Service Unavailable  | Server is down or overloaded           |


# What is a REST API?
A REST API (Representational State Transfer API) is a way for two systems — like a frontend and a backend — to talk to each other over the internet using HTTP requests.

What does the frontend send?
For GET, it just asks and maybe adds filters like ?age=20.<br>

For POST/PUT/PATCH, it sends data in JSON format, like:
{
  "name": "Lahari",
  "email": "lahari@example.com"
}

**REST APIs are stateless: every request must contain everything needed (the server doesn't remember your last request).**

| Action         | URL         | Method | What It Does             |
| -------------- | ----------- | ------ | ------------------------ |
| View all users | `/users`    | GET    | Returns a list           |
| View 1 user    | `/users/12` | GET    | Returns user with ID 12  |
| Add a user     | `/users`    | POST   | Adds a new user          |
| Update a user  | `/users/12` | PUT    | Replaces user with ID 12 |
| Delete a user  | `/users/12` | DELETE | Deletes that user        |

# Middleware

A middleware is a function in Express that sits in the middle of the request and response cycle. It receives the req (request), res (response), and a next function, and can do things like:

Modify the request or response, End the request–response cycle, Pass control to the next middleware or route


 Why Use Middleware?
For shared logic across routes (e.g., logging, auth)

For parsing data from the request body

For security, validation, and error handling

To add or modify headers

To handle CORS, static files, etc.

### Types

1. Application-Level Middleware<br>

Middleware that applies to all or specific routes using app.use() or app.METHOD().

Syntax:
```
app.use((req, res, next) => {
  console.log("Logging every request");
  next();
});
```
When to use:
Logging

Global validation

Authentication checks

Setting common headers


 2. Router-Level Middleware

Same as application-level, but attached to a Router instance instead of app.

 Syntax:
```
const router = express.Router();

router.use((req, res, next) => {
  console.log("Router-level middleware");
  next();
});
```
When to use:
Modular route-specific logic

Middleware that applies only to certain grouped routes


3. Built-In Middleware

Middleware functions that come with Express.

 Syntax:
```
app.use(express.json()); // Parse JSON body
app.use(express.urlencoded({ extended: true })); // Parse form data
app.use(express.static('public')); // Serve static files
```
When to use:
To handle form and JSON data<br>
To serve static CSS, JS, HTML files<br>

 4. Third-Party Middleware<br>
    Middleware provided by external npm packages.<br>

 Syntax:
 ```
const cors = require('cors');
app.use(cors());

const morgan = require('morgan');
app.use(morgan('dev'));

```
For logging, security, headers, performance, validation

 Popular Libraries:<br>
Package	-> Purpose<br>
cors	-> Enable cross-origin requests<br>
morgan	-> Log requests<br>
helmet	-> Secure headers<br>
cookie-parser-> 	Parse cookies<br>

 5. Error-Handling Middleware

Special middleware that catches errors across your app.<br>
 Syntax:
```
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```
When to use:
To handle validation errors<br>
To catch and respond to unhandled exceptions<br>
To avoid repeating try-catch in every route<br>

Must include four parameters: (err, req, res, next)


| Type              | Method Used           | Use Case                        |
| ----------------- | --------------------- | ------------------------------- |
| Application-level | `app.use()`           | Global logic like logging, auth |
| Router-level      | `router.use()`        | Modular route grouping          |
| Built-in          | `express.json()` etc. | Parsing, static files           |
| Third-party       | `app.use(package)`    | Logging, security, validation   |
| Error-handling    | `app.use((err,...))`  | Centralized error handling      |


 # What is MongoDB?
A NoSQL database (non-relational)
Stores data as collections of documents
Each document is a JSON-like object (called BSON)
Highly scalable, flexible, and used in modern web apps

Database holds collections just like a table but its not actually in table but in the form of document whuch holds key value pair inside a document known as field. Mongo internally uses Binary JSON format.

# What is Mongoose?

An ODM (Object Data Modeling) library for MongoDB + Node.js
Allows defining schemas to structure your data
Adds built-in validation and query features


# Defining a Schema
```
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  age: Number,
  email: { type: String, unique: true },
  createdAt: { type: Date, default: Date.now }
});
```
Creating a model - this creats a collection called users we include this in a file with schema
```
const User = mongoose.model('User', userSchema);
```
| Option       | Use for...                                 |
| ------------ | ------------------------------------------ |
| `type`       | Data type of the field                     |
| `required`   | Make the field mandatory                   |
| `default`    | Set default value                          |
| `unique`     | Prevent duplicate entries                  |
| `min`, `max` | Number limits                              |
| `enum`       | Accept only certain values (like dropdown) |
| `validate`   | Custom validation logic                    |


