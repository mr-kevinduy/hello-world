# Express

```JS
const express = require('express');
const app = express();
```

## Middleware
1. Application Level

```JS
app.use(function(req, res, next) {
    next();
});

app.get(function(req, res, next) {
    next();
}, function(req, res) {
    // Handler function (Middleware system).
    res.send('OK');
})
```

2. Router Level

```JS
const router = app.Router();

router.use(function(req, res, next) {
    if (!req.headers['x-auth']) return next('router');

    next();
});

router.get('/', function(req, res) {
    res.send('Welcome!!!');
});

app.get('/admin', router, function(req, res) {
    res.sendStatus(401);
});
```

3. Error-handling Middleware

```JS
app.use(function(err, req, res, next) {
    console.log(err.stack);
    res.status(500).send('Something broken!');
})
```

4. Build-in Middleware
    - express.static
    - express.json . Available in Express v4.16.0
    - express.urlencoded . Available in Express v4.16.0

```JS
express.json({
    inflate: true, // [Boolean]
    limit: '100kb', // [Mixed] Maximum request body size.
    reviver: null, // [Function]
    strict: true, // [Boolean]
    type: 'application/json', // [Mixed] '*/*' or '*/json'
    verify: undefined // Function
});

express.static(root, [options]);
```

5. Thirt-party Middleware

```Shell
$ npm install cookie-parser
$ npm install compression
...
```

More:
- Middleware: [https://expressjs.com/en/resources/middleware.html](https://expressjs.com/en/resources/middleware.html)
- Express: [https://expressjs.com/en/4x/api.html](https://expressjs.com/en/4x/api.html)