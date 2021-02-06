## NOSQL Query Injection

Sanitize data using the npm package called express-mongo-sanitize.

### Installation

```npm install express-mongo-sanitize```

### Usage

```
const app = require('express')
const mongoSanitize = require('express-mongo-sanitize');

const app = express();

app.use(mongoSanitize())
```

# Reference

 - [1](https://www.freecodecamp.org/news/express-js-security-tips/)