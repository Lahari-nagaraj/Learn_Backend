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

