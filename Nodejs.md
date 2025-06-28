# Learn_Backend


## What is Node.js?
Node.js is a runtime environment that lets you run JavaScript outside the browser.

It’s built on Chrome’s V8 engine and is asynchronous, event-driven, and non-blocking.

Used to build servers, APIs, CLI tools, and real-time apps.

### Setting up
```
# To install
node -v
npm -v

# Run a file
node index.js
```
### Core Modules in Node.js
Core modules are built into Node.js and do not require installation. You can use them with require('module-name'). They're optimized for performance and are essential for system-level and server-side tasks.
#### Few examples
Module -	Purpose
fs	-File system access<br>
http-	Creating servers<br>
os	-System info<br>
path-	Work with file paths <br>
events-	Handle custom events <br>
crypto-	Generate hashes, tokens<br>
url-	Parse/format URLs<br>

### First web server without express
```
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello World');
});

server.listen(3000, () => {
    console.log('Server running on port 3000');
});
```
### Then by use express?
1.Easier routing<br>
2.Middleware support<br>
3.Controllers<br>
4.Easy and automatic parsing of incoming JSON<br>
5 Supports 3rd party ecosystem like cors, express-validation,passport<br>
6 error handling<br>


### npm and package.json


#### What is npm?

- **npm** stands for **Node Package Manager**<br>
- It’s the **default package manager** for Node.js<br>
- Used to **install, manage, and publish** JavaScript packages<br>
- The world's **largest software registry**<br>

####  Common npm Commands:

| Command                | Purpose                                 |
|------------------------|------------------------------------------|
| `npm init`             | Creates a `package.json` (asks questions) |
| `npm init -y`          | Creates default `package.json` instantly |
| `npm install <pkg>`    | Installs a package (adds to dependencies) |
| `npm uninstall <pkg>`  | Removes a package                        |
| `npm install`          | Installs all dependencies in `package.json` |
| `npm install -g <pkg>` | Installs package globally               |

---

####  What is `package.json`?

`package.json` is a metadata file that defines your project and its dependencies.

### Modules and Exports 

Node.js uses the **CommonJS module system**, where each file is a separate **module**. This allows you to organize code into reusable components.

#### What is a Module?

A **module** in Node.js is simply a JavaScript file.  
Each file has its own **scope** — variables and functions defined inside won’t leak globally.

#### Types of Modules

1. **Core Modules** – Built-in (`fs`, `path`, `http`, etc.)<br>
2. **Local Modules** – Files you create (e.g., `math.js`)<br>
3. **Third-Party Modules** – Installed via `npm` (e.g., `express`)<br>

#### Exporting from a Module

Use `module.exports` to export **functions**, **objects**, or **variables**.


#### `require` vs `import` 

In Node.js, both `require` and `import` are used to include modules, but they are based on different module systems and have key differences.

#### Basic Differences

| Feature            | `require` (CommonJS)                  | `import` (ES Modules)                     |
|-------------------|----------------------------------------|-------------------------------------------|
| Module System     | CommonJS                               | ECMAScript Modules (ESM)                  |
| Syntax            | `const fs = require('fs')`             | `import fs from 'fs'`                     |
| File Type         | Works in `.js` files by default        | Needs `.mjs` or `"type": "module"`        |
| Import Timing     | Can be used dynamically                | Must be at top-level only                 |
| Export Syntax     | `module.exports = value`               | `export default`, `export { ... }`        |
| Support           | Default in all Node.js versions        | Fully supported in Node.js v14+           |


- Use **`require`** if you're building a regular Node.js backend with default setup.
- Use **`import`** if you're working with modern tooling (e.g., React, TypeScript, Vite), or you explicitly set:
  - `"type": "module"` in your `package.json`, or
  - Use `.mjs` file extensions.

#### What is `nodemon`?

**nodemon** is a dev tool that automatically restarts your Node.js server **whenever a file changes**. It makes development faster and smoother.

 #### What is dotenv?
dotenv is a module that loads environment variables from a .env file into process.env.
To keep sensitive data (API keys, DB credentials) out of your code.


### HTTP vs HTTPS

#### What is HTTP?

**HTTP** stands for **HyperText Transfer Protocol**. It is the protocol used to transfer data between a client (browser) and a server.

- It defines **how data is requested and transferred** (e.g., viewing a website).
- Data is sent in **plain text**, so it can be intercepted.
 Use HTTP when:
You're in a local development environment

Testing simple servers without sensitive data

Learning/practicing with no login, payment, or API keys involved

#### What is HTTPS?

**HTTPS** stands for **HyperText Transfer Protocol Secure**. It is the **secure version of HTTP**.
- **SSL/TLS encryption** to secure communication.
- **Digital certificates** (issued by Certificate Authorities).
-  Use HTTPS when:
Your app deals with user credentials, payments, or private data

You're deploying to production

You're using authentication systems (JWT, OAuth)

You want to prevent man-in-the-middle attacks

#### Major Differences

| Feature          | HTTP                            | HTTPS                                |
|------------------|----------------------------------|----------------------------------------|
|  Security       | Not secure (plain text)          | Encrypted (via SSL/TLS)                |
|  Encryption     |  None                          |  Yes                                 |
| Authentication |  None                          |  Validates server identity           |
|  Port           | 80                              | 443                                    |
|  URL Format     | `http://example.com`            | `https://example.com`                  |
| Vulnerability   | Prone to data sniffing, MITM    | Safe from man-in-the-middle attacks   |
|  SEO & Trust     | Not preferred by browsers       | Required for modern browsers (secure padlock ) |


#  Request-Response Lifecycle 

1. **Client Sends Request**: A browser or frontend sends an HTTP request to the server with method, URL, headers, and optional body.

2. **Server Receives Request**: Node.js server listens on a port and receives the incoming request.

3. **Middleware Runs** *(Express only)*: Middleware functions process the request (e.g., parsing JSON, logging, authentication).

4. **Route Handler Executes**: Based on the request path and method, the matching handler runs logic and prepares a response.

5. **Response is Sent**: The server sends back status, data, and headers.

6. **Client Receives Response**: The frontend/browser processes the response and updates the UI accordingly.




#### JSON (JavaScript Object Notation)
- A lightweight format for exchanging data between client and server.
- Data is structured in key-value pairs.
- Easy to parse and generate in JavaScript.

Example structure:
```json
{ "name": "Lahari", "age": 20 }
```

 #### HTTP Headers
Headers are metadata sent with requests and responses.

They describe what’s being sent, how to handle it, and client/server behavior.

##### Common headers:

Content-Type: Format of the data (e.g., application/json)<br>
Authorization: Carries tokens for secured APIs<br>
Accept: Specifies expected response format<br>

#### Content-Type
Tells the server or client what type of data is being sent.<br>

application/json – JSON data<br>
text/html – HTML content<br>
application/x-www-form-urlencoded – Form data (e.g., from HTML forms)<br>
multipart/form-data – Used for file uploads<br>

