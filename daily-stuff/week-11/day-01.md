# Day 01

What we covered today:

* Singly Linked Lists continued
* Burning Airline Backend - Node.js, express & mongoDB

### Warmup <a id="warmup"></a>

* [Wordy Calculator](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week11/day01_wordy_calculator)

### Codealongs  <a id="codealongs"></a>

* [Singly Linked Lists](https://github.com/textchimp/wdi-29/tree/master/week10/singly-linked-lists)
* [Burning Airlines - Express & noDB](https://github.com/textchimp/wdi-29/tree/master/week10/node-servers/ba-express-server-no-db)
* [​Burning Airlines - Express & mongoDB](https://github.com/textchimp/wdi-29/tree/master/week10/node-servers/ba-express-server-mongodb)

## Burning Airline - Express server with no DB <a id="express"></a>

We've already created a full stack web application with Vue front end and Rails backend, this time we will replace the Rails back end with Node.js. Our Burning Airline front end stays the same:

```bash
mkdir ba-express-server-no-db
cd ba-express-server-no-db
# Use npm init to create package.json
# skip the 'wizard'-style Q&A process with the -y flag
ba-express-server-no-db$ npm init -y 
Wrote to /Users/linna/wdi/classwork/week10/node-servers/ba-express-server-no-db/package.json:

{
  "name": "ba-express-server-no-db",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
ba-express-server-no-db$ touch server.js
```

### Express

Express is a light-weight web application framework to help organise your web application into an MVC architecture on the server side. You can use a variety of choices for your templating language \(like EJS, Jade, and Dust.js\). EJS would be a similar syntax to what we're use to with Rails erb.html files.

You can then use a database like MongoDB with Mongoose \(for modeling\) to provide a backend for your Node.js application. Express.js basically helps you manage everything, from routes, to handling requests and views.

### _Installing Express_ <a id="installing-express"></a>

Navigate to the root directory of your project and install express.

```bash
npm install --save express
```

Back to `server.js`, create a fake database:

```javascript
const flights = [
  {
    id: 1,
    flight_number: '123',
    depature_date_formatted: "Tue 25 December, 08:00am",
    origin: 'SYD',
    destination: 'SFO',
    plane: { name: '737', rows: 40, cols: 4 }
  },
  {
    id: 1,
    flight_number: '456',
    depature_date_formatted: "Wed 26 December, 02:00am",
    origin: 'SYD',
    destination: 'SFO',
    plane: { name: '737', rows: 60, cols: 6 }
  },
  {
    id: 1,
    flight_number: '789',
    depature_date_formatted: "Tue 30 December, 09:00am",
    origin: 'SYD',
    destination: 'SIN',
    plane: { name: '757', rows: 80, cols: 8 }
  },
];

const reservations = {};
const user_reservations = {};
```

`require` function is the easiest way to include modules that exist in separate files. The basic functionality of `require` is that it reads a javascript file, executes the file, and then proceeds to return the exports object.

```javascript
const express = require('express');
const app = express();

const server = app.listen(3000, () => {
  console.log("Server listening on port 3000...");
});
```

Now run `node server.js` from the terminal,  we should be able to get the following output:

```javascript
ba-express-server-no-db$ node server.js
Server listening on port 3000...
```

### Enable server restart on file changes <a id="enable-server-restart-on-file-changes"></a>

Any changes you make to your Express website are currently not visible until you restart the server. It quickly becomes very irritating to have to stop and restart your server every time you make a change, so it is worth taking the time to automate restarting the server when needed. One of the easiest such tools for this purpose is [nodemon](https://github.com/remy/nodemon). This is usually installed globally \(as it is a "tool"\), but here we'll install and use it locally as a developer dependency, so that any developers working with the project get it automatically when they install the application. Use the following command in the root directory for the skeleton project:

```bash
npm install --save nodemon
```

### Using CORS in Express

Cross-origin resource sharing \(CORS\) allows AJAX requests to skip the same-origin policy and access resources from remote hosts. The easiest way to get CORS working in Express is by using the [cors npm module](https://www.npmjs.com/package/cors). To use it, just run the following command in the root directory to install it:

```bash
npm install --save cors
```

If you open your project's `package.json` file, you'll now see a new section with this dependency:

```javascript
  "dependencies": {
    "cors": "^2.8.5",
    "express": "^4.16.4",
    "mongodb": "^3.1.10",
    "nodemon": "^1.18.6"
  }
```

Because the tool isn't installed globally we can't launch it from the command line \(unless we add it to the path\) but we can call it from an NPM script because NPM knows all about the installed packages. Find the the `scripts` section of your `package.json`. Initially it will contain one line, which begins with `"start"`. Update it by putting a comma at the end of that line, and adding the `"start"` and `"server"`  as below: 

```javascript
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js",
    "server": "nodemon server.js"
  },
```

Now run the `npm run server`,  if you edit any file in the project the server will restart \(or you can restart it by typing `rs` on the command prompt at any time\). You will still need to reload the browser to refresh the page.

```bash
ba-express-server-no-db$ npm run server
> ba-express-server-no-db@1.0.0 server /Users/linna/wdi/classwork/week10/node-servers/ba-express-server-no-db
> nodemon server.js

[nodemon] 1.18.6
[nodemon] to restart at any time, enter `rs`
[nodemon] watching: *.*
[nodemon] starting `node server.js`
Server listening on port 3000...
rs
[nodemon] starting `node server.js`
Server listening on port 3000...
```

We now have to call `npm run` rather than just `npm start`, because `start` is actually an NPM command that is mapped to the named script. We could have replaced the command in the start script but we only want to use nodemon during development, so it makes sense to create a new script command.

Then import the `cors` :

```javascript
const express = require('express');
//the ajax request from 'http://localhost:8080' to 'http://localhost:3000/flights/1' has been blocked due to same-origin policy

const cors = require('cors');
const app = express();

// allow cross-origin-requests (avoid CORS error )
app.use(cors());
// CORS is now enabled
```

To get the specific flight via its id, we could write:

```javascript
app.get('/flights/:id', (req, res) => {
  console.log(req.params);

  //we want the integer, right now it is string
  const requestedID = parseInt(req.params.id);

  // .find will loop over all the flights and find the specified flight by id, it return the first one
  // find the flight object from the array whose id field matches the ID from the URL
  const flight = flights.find( f => f.id === requestedID);
  // console.log(flight);
  res.json( {flight, reservations, user_reservations });
});
```

To search flights via origin and destination, it would be like:

```javascript
// i.e. GET /flights/SYD/SFO, we should check req.params.origin === "SYD", req.params.destination === "SFO"
app.get('/search/:origin/:destination', (req, res) => {
 
  const {origin, destination} = req.params; //ES6 object destructuring
 
  // The filter() method creates an array filled with all array elements that pass the test
  const results = flights.filter( f => f.origin === origin && f.destination === destination);
  res.json( results );
});
```

For POST request, firstly we need to be able to retrieve POST query parameters. From Express 4.16.0 we could use `express.json()` :

```javascript
app.use(express.json());       // to support JSON-encoded bodies
app.use(express.urlencoded()); // to support URL-encoded bodies

app.post('/booking', (req, res) => {
  console.log("POST to /booking", req.body);
})
```

To test a booking request from front end to back end, firstly we go to `http://localhost:8080/#/flights/1` and click a seat from the seating map. You should see the following output from the terminal:

```bash
POST to /booking { row: 1, col: 1, flight_id: 1 }
```

## MongoDB <a id="express"></a>

### What is mongoDB?

MongoDB is a document database with the scalability and flexibility that you want with the querying and indexing that you need. It stores data in flexible, JSON-like documents, meaning fields can vary from document to document and data structure can be changed over time. The document model maps to the objects in your application code, making data easy to work with.

### _Installing mongoDB_ <a id="installing-express"></a>

 Install mongoDB from anywhere using HomeBrew:

```bash
brew install mongodb
```

To load and start the MongoDB service, run : 

```bash
brew services start mongodb
```

For more information about how to install [MongoDB](https://www.mongodb.org/) using [Homebrew](http://brew.sh/), [click here](https://gist.github.com/nrollr/9f523ae17ecdbb50311980503409aeb3).

### _Working with the `mongo` Shell_

You can run [`mongo`](https://docs.mongodb.com/manual/reference/program/mongo/#bin.mongo) shell without any command-line options to connect to a [MongoDB](https://docs.mongodb.com/manual/reference/program/mongod/) instance running on your localhost with _default port_ 27017:

```bash
anyfolder$ mongo
MongoDB shell version v3.6.5
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.6.5
Mongo-Hacker 0.0.14
Server has startup warnings:
2018-11-17T08:03:02.131+1100 I CONTROL  [initandlisten]
2018-11-17T08:03:02.131+1100 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2018-11-17T08:03:02.131+1100 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2018-11-17T08:03:02.131+1100 I CONTROL  [initandlisten]
2018-11-19T21:41:34.826+1100 E QUERY    [thread1] uncaught exception: don't know how to show [automationNotices]
```

To display the database you are using, type `db`:

```text
MacBook-Pro(mongod-3.6.5) test> db
test
```

Install mongo-hacker to give us different text colours and highlighting inside mongoDB:

```bash
npm install -g mongo-hacker
```

If we want to ceate a ba database we could just run the following commands from any repo:

```bash
anyfolder$ mongo ba
MacBook-Pro(mongod-3.6.5) ba> db
ba
```

A few common commands:

```javascript
MacBook-Pro(mongod-3.6.5) ba> show collections
MacBook-Pro(mongod-3.6.5) ba> db.flights.insertOne({ a:1 })
{
  "acknowledged": true,
  "insertedId": ObjectId("5bf23342d6431cf93a1aa9a5")
}

MacBook-Pro(mongod-3.6.5) ba> db.flights.find()
{
  "_id": ObjectId("5bf23342d6431cf93a1aa9a5"),
  "a": 1
}
Fetched 1 record(s) in 54ms
MacBook-Pro(mongod-3.6.5) ba> db.flights.insertOne({flight_number: '123', origin: 'SYD', destination: 'SFO', capacity: 300})
{
  "acknowledged": true,
  "insertedId": ObjectId("5bf2350753dae8965ada71d4")
}
MacBook-Pro(mongod-3.6.5) ba> db.flights.find()
{
  "_id": ObjectId("5bf23342d6431cf93a1aa9a5"),
  "a": 1
}
{
  "_id": ObjectId("5bf2350753dae8965ada71d4"),
  "flight_number": "123",
  "origin": "SYD",
  "destination": "SFO",
  "capacity": 300
}
Fetched 2 record(s) in 2ms

MacBook-Pro(mongod-3.6.5) ba> db.flights.insertOne({flight_number: '456', origin: 'SYD', destination: 'SIN', capacity: 500})
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({flight_number: "123"})
{
  "_id": ObjectId("5bf2350753dae8965ada71d4"),
  "flight_number": "123",
  "origin": "SYD",
  "destination": "SFO",
  "capacity": 300
}
Fetched 1 record(s) in 9ms

# db.flights.find() is like Flight.where in ActiveRecord
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({flight_number: "123"})
{
  "_id": ObjectId("5bf2350753dae8965ada71d4"),
  "flight_number": "123",
  "origin": "SYD",
  "destination": "SFO",
  "capacity": 300
}
Fetched 1 record(s) in 9ms

MacBook-Pro(mongod-3.6.5) ba> db.flights.find({origin: "SYD"})
{
  "_id": ObjectId("5bf2350753dae8965ada71d4"),
  "flight_number": "123",
  "origin": "SYD",
  "destination": "SFO",
  "capacity": 300
}
{
  "_id": ObjectId("5bf236ec53dae8965ada71d5"),
  "flight_number": "456",
  "origin": "SYD",
  "destination": "SIN",
  "capacity": 500
}
Fetched 2 record(s) in 1ms

# additional condition, $ dollar sign is a special mongo database query
# $gt means greater than
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({origin: "SYD", capacity: { $gt: 400 } })
{
  "_id": ObjectId("5bf236ec53dae8965ada71d5"),
  "flight_number": "456",
  "origin": "SYD",
  "destination": "SIN",
  "capacity": 500
}
Fetched 1 record(s) in 8ms

# $lt means less than
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({origin: "SYD", capacity: { $lt: 500 } })
{
  "_id": ObjectId("5bf2350753dae8965ada71d4"),
  "flight_number": "123",
  "origin": "SYD",
  "destination": "SFO",
  "capacity": 300
}
Fetched 1 record(s) in 8ms

MacBook-Pro(mongod-3.6.5) ba> db.flights.insertOne({flight_number: '789', origin: 'SYD', destination: 'SIN', capacity: 600, plane: { rows: 30, cols:6 } })
{
  "acknowledged": true,
  "insertedId": ObjectId("5bf2394253dae8965ada71d6")
}

# you could create association when you created the flight
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({flight_number: '789'})
{
  "_id": ObjectId("5bf2394253dae8965ada71d6"),
  "flight_number": "789",
  "origin": "SYD",
  "destination": "SIN",
  "capacity": 600,
  "plane": {
    "rows": 30,
    "cols": 6
  }
}
Fetched 1 record(s) in 8ms

# To find a nested data
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({ 'plane.rows': 30 })
{
  "_id": ObjectId("5bf2394253dae8965ada71d6"),
  "flight_number": "789",
  "origin": "SYD",
  "destination": "SIN",
  "capacity": 600,
  "plane": {
    "rows": 30,
    "cols": 6
  }
}
Fetched 1 record(s) in 1ms

# To delete a database
MacBook-Pro(mongod-3.6.5) ba> db.flights.remove({"a": 1})
Removed 1 record(s) in 52ms
WriteResult({
  "nRemoved": 1
})

# when you search, the order of the structure matters
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({ plane: {rows: 30}})
Fetched 0 record(s) in 1ms
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({ plane: {rows: 30, cols: 6}})
{
  "_id": ObjectId("5bf2394253dae8965ada71d6"),
  "flight_number": "789",
  "origin": "SYD",
  "destination": "SIN",
  "capacity": 600,
  "plane": {
    "rows": 30,
    "cols": 6
  }
}
Fetched 1 record(s) in 1ms
MacBook-Pro(mongod-3.6.5) ba> db.flights.find({ plane: {cols: 6, rows: 30}})
Fetched 0 record(s) in 0ms

MacBook-Pro(mongod-3.6.5) ba> exit
bye
```

For more information, check mongoDB manual.

## Burning Airline - Express server with mongoDB <a id="express"></a>

Create a new folder inside classwork:

```bash
mkdir ba-express-server-mongodb
cd ba-express-server-mongodb
ba-express-server-mongodb$ npm init -y
Wrote to /Users/linna/tmp/ba-express-server-mongodb/package.json:

{
  "name": "ba-express-server-mongodb",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
ba-express-server-mongodb$ atom .
```

Now create a new file called `seeds-flights.js` and add our seed data:

```javascript
[
  {
    'flight_number': '123',
    'origin': 'SYD',
    'destination': 'SFO',
    'departure_date_formatted': ISODate('2018-12-25T20:20:00Z'),
    'plane': { 'name': '757', 'rows': 50, 'cols': 8 },
    'reservations': [
      {'row': 10, 'col': 3},
      {'row': 11, 'col': 2}
    ]
  },
  {
    'flight_number': '456',
    'origin': 'SYD',
    'destination': 'SFO',
    'departure_date_formatted': ISODate('2018-12-30T12:12:00Z'),
    'plane': { 'name': '737', 'rows': 40, 'cols': 4 },
    'reservations': [
      {'row': 1, 'col': 2, 'passenger': {'name': 'test guy', 'email': 'test@guy.com'} },
      {'row': 2, 'col': 3}
    ]
  },
  {
    'flight_number': '789',
    'origin': 'SYD',
    'destination': 'SIN',
    'departure_date_formatted': ISODate('2018-12-31T23:23:23Z'),
    'plane': { 'name': '757', 'rows': 40, 'cols': 4 },
    'reservations': [
      {'row': 5, 'col': 6},
      {'row': 5, 'col': 7}
    ]
  }
]
```

Create package.json and install essential packages:

```javascript
ba-express-server-mongodb$ npm init -y
Wrote to /Users/linna/tmp/ba-express-server-mongodb/package.json:

{
  "name": "ba-express-server-mongodb",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": ""
}


ba-express-server-mongodb$ npm install --save express mongodb cors nodemon
```

Add the following code in your `script:`

```javascript
{
  "name": "ba-express-server-mongodb",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "seed": "mongoimport --db ba --collection flights --drop --jsonArray --file seeds-flights.js",
    "server": "nodemon server.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cors": "^2.8.5",
    "express": "^4.16.4",
    "mongodb": "^3.1.10",
    "nodemon": "^1.18.6"
  }
}

```

Run `npm run seed` will import our seed data:

```javascript
burning-airlines-server-express-mongodb (master)$ npm run seed

> burning-airlines-server-express-mongodb@1.0.0 seed /Users/linna/wdi/classwork/week10/node-servers/burning-airlines-server-express-mongodb
> mongoimport --db ba --collection flights --drop --jsonArray --file ba-flights.js

2018-11-19T22:15:10.653+1100	connected to: localhost
2018-11-19T22:15:10.656+1100	dropping: ba.flights
2018-11-19T22:15:10.795+1100	imported 3 documents
```

#### 

### Further Reading

* [Express](https://expressjs.com/)
* [mongo Shell Quick Reference](https://docs.mongodb.com/manual/reference/mongo-shell/)
* [MongoDB CRUD Operations](https://docs.mongodb.com/manual/crud/)
* [NoSQL vs Relational databases](https://www.youtube.com/watch?v=qI_g07C_Q5I)​

