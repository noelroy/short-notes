# Best Practices and tips

### Import ENV constants from file

Use npm package `dotenv`.
By default, it looks for a .env file in the root dir.

#### Installation

```bash
npm i dotenv
```

#### Usage

```js
require('dotenv').config()
require('dotenv').config({ path: './config/.env' })  # If a file has to be specified
```

### Middlewares

The order of middlewares are important.
Middleware takes in 3 arguments. Always call `next()` inside a middleware

```js
app.use(function(req,res,next){
    next();
})
```

### Default error handler

Node has a default error handler. If we want to modify the behaviour of this handler define a middleware at the end as follows

```js
app.use(function(error, req, res, next){
    
})
```

Use next function to redirect all error to the error handler.

```js
return next(new Error("Invalid Id"))
```

### Separate Express 'app' and 'server'

Separate API declaration from network related configurations. This allows testing the API in-process, without performing network calls.

```js
const app = require('../app')
const http = require('http')

const PORT = process.env.PORT || 5000
app.set('port', PORT)

const server = http.createServer(app)
```

### Proxying requets

To have out client server proxy out API requests to API Server , we need to add the following to client/package.json
```
"proxy": "http://localhost:5000/"
```

### Concurrently

Concurrently is a utility for running multiple processes. This can be used to run both server and client using a single command.

```sh
#concurrently command1 command2
concurrently "npm run server" "cd client && npm start"
```

## Reference

[Node Best Practices](https://github.com/goldbergyoni/nodebestpractices)