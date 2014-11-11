Heroku Buildpack for Node.js, Gulp, Bower and Sass
========================================

Usage
-----

- Set your Heroku app's buildpack URL to `https://github.com/Gertrwde/heroku-buildpack-nodejs-bower-gulp-sass.git`. To be safe, you should really fork this and use your fork's URL.
- Run `heroku labs:enable user-env-compile` to enable environment variable support
- Run `heroku config:set NODE_ENV=production` to set your environment to `production` (or any other name)
- Add a Gulp task called `heroku` that builds your app
- Install the dependenies for serving the app: `npm install gzippo express morgan --save`
- Create a simple web server in the root called `heroku_web.js`:

```javascript
var gzippo = require('gzippo');
var logger = require('morgan');
var express = require('express');
var app = express();

app.use(logger('dev'));
app.use(gzippo.staticGzip("" + __dirname + "/build"));
app.listen(process.env.PORT || 5000);
```

- Add a single line `Procfile` to the root to serve the app via node:

```
web: node heroku_web.js
```

Credits
-------

Inspired by [Deploying a Yeoman/Angular app to Heroku](http://www.sitepoint.com/deploying-yeomanangular-app-heroku/).

Forked from [heroku-buildpack-nodejs-gulp](https://github.com/timdp/heroku-buildpack-nodejs-gulp).

Which was forked from [heroku-buildpack-nodejs](https://github.com/heroku/heroku-buildpack-nodejs).

Heavily based on [heroku-buildpack-nodejs-grunt](https://github.com/mbuchetics/heroku-buildpack-nodejs-grunt).
