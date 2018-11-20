# Day 02

What we covered today:

* Express
* Javascript - Github Search
  * Webpack

#### Warmup

* ​[Markov Text​](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week11/day02_markov_text)

#### Codealongs

* [Express Example](https://github.com/textchimp/wdi-29/tree/master/week10/node-servers/express-generator-example-project)
* [​Webpack- React​](https://github.com/textchimp/wdi-29/tree/master/week11/webpack-react-github-app)

## Express - continued <a id="express"></a>

### _Installing Express_ <a id="installing-express"></a>

Navigate to the root directory of your project and install express.

```bash
npm install -g express-generator
```

We now have access to the express commands. Create your app using express.

```bash
express hello-world
cd hello-world/
npm install
```

Set an environment var of debug

```bash
DEBUG=hello-world:* npm start
```

Open your browser and navigate to `http://localhost:3000/`.

Open your project in text editor

```bash
atom .
```

If you check the `app.js` file you will see all the dependancies that are being required. In the views folder there is an `index.jade` file that is the `erb.html` equivalent for express. We don't actually want to be using .jade as we're more accustom to erb.

Using `express -e` will generate a new project with `.ejs` file in the view folder.

```bash
cd ..
express -e hello-world
npm install
```

Now check the view and we will have a new type of file that look more closely to what we're use to `index.ejs`

Shutdown the previous server with `ctrl + c` and start a new one.

```bash
DEBUG=hello-world:* npm start
```

### _Enable server restart on file changes - continued_ <a id="enable-server-restart-on-file-changes"></a>

Any changes you make to your Express website are currently not visible until you restart the server. It quickly becomes very irritating to have to stop and restart your server every time you make a change, so it is worth taking the time to automate restarting the server when needed. One of the easiest such tools for this purpose is [nodemon](https://github.com/remy/nodemon). This is usually installed globally \(as it is a "tool"\), but here we'll install and use it locally as a developer dependency, so that any developers working with the project get it automatically when they install the application. Use the following command in the root directory for the skeleton project:

```bash
npm install --save-dev nodemon
```

If you open your project's package.json file you'll now see a new section with this dependency:

```javascript
"devDependencies": {
    "nodemon": "^1.12.1"
  }
```

Because the tool isn't installed globally we can't launch it from the command line \(unless we add it to the path\) but we can call it from an NPM script because NPM knows all about the installed packages. Find the the `scripts` section of your package.json. Initially it will contain one line, which begins with `"start"`. Update it by putting a comma at the end of that line, and adding the `"devstart"` line seen below:

```javascript
"scripts": {
    "start": "node ./bin/www",
    "devstart": "nodemon ./bin/www"
  },
```

We can now start the server in almost exactly the same way as previously, but with the `devstart` command specified:

```javascript
DEBUG=express-locallibrary-tutorial:* npm run devstart
```

* Note: Now if you edit any file in the project the server will restart \(or you can restart it by typing rs on the command prompt at any time\). You will still need to reload the browser to refresh the page.

We now have to call `npm run` rather than just `npm start`, because `start` is actually an NPM command that is mapped to the named script. We could have replaced the command in the start script but we only want to use nodemon during development, so it makes sense to create a new script command.

### _The generated project_ <a id="the-generated-project"></a>

Let's now take a look at the project we just created.

_Directory structure_

The generated project, now that you have installed dependencies, has the following file structure \(files are the items not prefixed with "/"\). The package.json file defines the application dependencies and other information. It also defines a startup script that will call the application entry point, the JavaScript file /bin/www. This sets up some of the application error handling and then loads app.js to do the rest of the work. The app routes are stored in separate modules under the routes/ directory. The templates are stored under the /views directory.

```text
/express-locallibrary-tutorial
    app.js
    /bin
        www
    package.json
    /node_modules
        [about 4,500 subdirectories and files]
    /public
        /images
        /javascripts
        /stylesheets
            style.css
    /routes
        index.js
        users.js
    /views
        error.pug
        index.pug
        layout.pug
```

The following sections describe the files in a little more detail.

### _package.json_ <a id="package-json"></a>

The package.json file defines the application dependencies and other information:

```javascript
{
  "name": "express-locallibrary-tutorial",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www",
    "devstart": "nodemon ./bin/www"
  },
  "dependencies": {
    "body-parser": "~1.18.2",
    "cookie-parser": "~1.4.3",
    "debug": "~2.6.9",
    "express": "~4.15.5",
    "morgan": "~1.9.0",
    "pug": "2.0.0-beta11",
    "serve-favicon": "~2.4.5"
  },
  "devDependencies": {
    "nodemon": "^1.12.1"
  }
}
```

The dependencies include the express package and the package for our selected view engine \(pug\). In addition, we have the following packages that are useful in many web applications:

* ​[body-parser](https://www.npmjs.com/package/body-parser): This parses the body portion of an incoming HTTP request and makes it easier to extract different parts of the contained information. For example, you can use this to read POST parameters.
* ​[cookie-parser](https://www.npmjs.com/package/cookie-parser): Used to parse the cookie header and populate req.cookies \(essentially provides a convenient method for accessing cookie information\).
* ​[debug](https://www.npmjs.com/package/debug): A tiny node debugging utility modelled after node core's debugging technique.
* ​[morgan](https://www.npmjs.com/package/morgan): An HTTP request logger middleware for node.
* ​[serve-favicon](https://www.npmjs.com/package/serve-favicon): Node middleware for serving a favicon \(this is the icon used to represent the site inside the browser tab, bookmarks, etc.\). The scripts section defines a "start" script, which is what we are invoking when we call npm start to start the server. From the script definition you can see that this actually starts the JavaScript file ./bin/www with node. It also defines a "devstart" script, which we invoke when calling npm run devstart instead. This starts the same ./bin/www file, but with nodemon rather than node.

```javascript
"scripts": {
    "start": "node ./bin/www",
    "devstart": "nodemon ./bin/www"
  },
```

### _www file_ <a id="www-file"></a>

The file /bin/www is the application entry point! The very first thing this does is require\(\) the "real" application entry point \(app.js, in the project root\) that sets up and returns the express\(\) application object.

```javascript
#!/usr/bin/env node
​
/**
 * Module dependencies.
 */
​
var app = require('../app');
```

* Note: require\(\) is a global node function that is used to import modules into the current file. Here we specify app.js module using a relative path and omitting the optional \(.js\) file extension.

The remainder of the code in this file sets up a node HTTP server with app set to a specific port \(defined in an environment variable or 3000 if the variable isn't defined\), and starts listening and reporting server errors and connections. For now you don't really need to know anything else about the code \(everything in this file is "boilerplate"\), but feel free to review it if you're interested.

### _app.js_ <a id="app-js"></a>

This file creates an express application object \(named app, by convention\), sets up the application with various settings and middleware, and then exports the app from the module. The code below shows just the parts of the file that create and export the app object:

```javascript
const express = require('express');
const app = express();
...
module.exports = app;
```

Back in the www entry point file above, it is this module.exports object that is supplied to the caller when this file is imported.

Lets work through the app.js file in detail. First we import some useful node libraries into the file using require\(\), including express, serve-favicon, morgan, cookie-parser and body-parser that we previously downloaded for our application using NPM; and path, which is a core Node library for parsing file and directory paths.

```javascript
const express = require('express');
const path = require('path');
const favicon = require('serve-favicon');
const logger = require('morgan');
const cookieParser = require('cookie-parser');
const bodyParser = require('body-parser');
```

Then we `require()` modules from our routes directory. These modules/files contain code for handling particular sets of related "routes" \(URL paths\). When we extend the skeleton application, for example to list all books in the library, we will add a new file for dealing with book-related routes.

```javascript
const index = require('./routes/index');
const users = require('./routes/users');
```

* Note: At this point we have just imported the module; we haven't actually used its routes yet \(this happens just a little bit further down the file\).

Next we create the app object using our imported express module, and then use it to set up the view \(template\) engine. There are two parts to setting up the engine. First we set the 'views' value to specify the folder where the templates will be stored \(in this case the sub folder /views\). Then we set the 'view engine' value to specify the template library \(in this case "pug"\).

```javascript
const app = express();
​
// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'pug');
```

The next set of functions call `app.use()` to add the middleware libraries into the request handling chain. In addition to the 3rd party libraries we imported previously, we use the `Express.static` middleware to get Express to serve all the static files in the directory `/public` in the project root.

```javascript
// uncomment after placing your favicon in /public
//app.use(favicon(path.join(__dirname, 'public', 'favicon.ico')));
app.use(logger('dev'));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));
```

Now that all the other middleware is set up, we add our \(previously imported\) route-handling code to the request handling chain. The imported code will define particular routes for the different parts of the site:

```javascript
app.use('/', index);
app.use('/users', users);
```

* Note: The paths specified above \(`'/'` and `'/users'`\) are treated as a prefix to routes defined in the imported files. So for example if the imported users module defines a route for `/profile`, you would access that route at `/users/profile`.

The last middleware in the file adds handler methods for errors and HTTP 404 responses.

```javascript
// catch 404 and forward to error handler
app.use(function(req, res, next) {
  var err = new Error('Not Found');
  err.status = 404;
  next(err);
});
​
// error handler
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get('env') === 'development' ? err : {};
​
  // render the error page
  res.status(err.status || 500);
  res.render('error');
});
```

The Express application object \(app\) is now fully configured. The last step is to add it to the module exports \(this is what allows it to be imported by /bin/www\).

```javascript
module.exports = app;
```

The route file /routes/users.js is shown below \(route files share a similar structure, so we don't need to also show index.js\). First it loads the express module, and uses it to get an `express.Router` object. Then it specifies a route on that object, and lastly exports the router from the module \(this is what allows the file to be imported into `app.js`\).

```javascript
const express = require('express');
const router = express.Router();
​
/* GET users listing. */
router.get('/', function(req, res, next) {
  res.send('respond with a resource');
});
​
module.exports = router;
```

The route defines a callback that will be invoked whenever an HTTP `GET` request with the correct pattern is detected. The matching pattern is the route specified when the module is imported \(`'/users'`\) plus whatever is defined in this file \(`'/'`\). In other words, this route will be used when an URL of `/users/` is received.

* Tip: Try this out by running the server with node and visiting the URL in your browser: `http://localhost:3000/users/`. You should see a message: 'respond with a resource'.

One thing of interest above is that the callback function has the third argument `'next'`, and is hence a middleware function rather than a simple route callback. While the code doesn't currently use the `next` argument, it may be useful in the future if you want to add multiple route handlers to the `'/'` route path.

### Views <a id="views"></a>

The views \(templates\) are stored in the /views directory \(as specified in app.js\) and are given the file extension .pug. The method Response.render\(\) is used to render a specified template along with the values of named variables passed in an object, and then send the result as a response. In the code below from /routes/index.js you can see how that route renders a response using the template "index" passing the template variable "title".

```javascript
/* GET home page. */
router.get('/', function(req, res) {
  res.render('index', { title: 'Express' });
});
```

The corresponding template for the above route is given below \(index.pug\). We'll talk more about the syntax later. All you need to know for now is that the title variable \(with value 'Express'\) is inserted where specified in the template.

```text
extends layout
​
block content
  h1= title
  p Welcome to #{title}
```

## Webpack - GitHub search

### _What is webpack?_

 ****[**Webpack**](https://webpack.js.org/) is a _static module bundler_ for modern JavaScript applications. When webpack processes your application, it internally builds a [dependency graph](https://webpack.js.org/concepts/dependency-graph/) which maps every module your project needs and generates one or more _bundles_.

```bash
mkdir project-name
cd project-name
npm init -y
```

```bash
npm install --save-dev babel-loader @babel/core @babel/preset-env webpack webpack-dev-server webpack-cli babel-plugin-transform-react-jsx babel-plugin-transform-object-rest-spread prop-types
npm install --save axios react react-dom react-router react-router-dom 
mkdir src dist
touch src/index.html src/index.js
mkdir src/components
touch webpack.config.js
```

Add the following 2 lines in your package.json file:

```javascript
// package.json
"scripts": {
   "build": "webpack --mode=production",
    "dev": "webpack-dev-server --progress --hot --inline --mode=development"
},
```

Add the following code into the corresponding files:

```javascript
// webpack.config.js
const path = require('path');
module.exports = {
  // starting point for the webpack build process:
  entry: './src',
  // specify what processing webpack should perform on our input files:
  module: {
    rules: [
      {
        test: /\.jsx?/i, // files which match this regex will be processed: .js or .jsx
        loader: 'babel-loader',
        options: {
          plugins: [
            ['transform-react-jsx']
          ]
        }
      }
    ]
  }, //module
  // where to put the transformed output from the processing stage:
  output: {
    path: path.join(__dirname, 'dist'),
    filename: 'bundle.js' // this is the file we need to load in our index.html
  },
  devtool: 'inline-source-map', // see errors in the original .jsx source files
  devServer: {
    // options to pass to the webpack dev server:
    contentBase: path.join(__dirname, 'src'),
    compress: true,
    historyApiFallback: true
  }
};
```

```markup
src/index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Hello World</title>
</head>
<body>
  <script src="/bundle.js" async></script>
</body>
</html>
```

```javascript
// src/index.js
import React from 'react';
import ReactDom from 'react-dom';
import { HashRouter as Router, Route } from 'react-router-dom';

import Home from './components/Home.jsx';
import Search from './components/Search.jsx';
import GitHubProfile from './components/GitHubProfile.jsx';

const Routes =  (
  <Router>
    <div>
      <Route exact path='/' component={ Home }/>
      <Route exact path='/search' component={Search} />
      <Route exact path='/details/:username' component={GitHubProfile} />
    </div>
  </Router>
);

ReactDom.render(Routes, document.getElementById('app'));
```

```javascript
// src/components/Home.js
import React, { Component } from 'react';
import { Link } from 'react-router-dom';

class Home extends Component {
  render(){
    return(
      <div>
        <h1>GitHub Search</h1>
        <Link to="/search"> {/* Navigate to a new React app route */}
          <button>Search for a user</button>
        </Link>
        <button>Random user</button>
      </div>
    );
  }
}

export default Home;

```



### Further Reading <a id="further-reading"></a>

* ​[Express](https://expressjs.com/)​
* ​[Express Tutorial](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/skeleton_website)​
* ​[Webpack](https://webpack.js.org/)​
* ​[Webpack Concepts](https://webpack.js.org/concepts/)​



