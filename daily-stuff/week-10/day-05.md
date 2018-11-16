# Day 05

What we covered today:

* Singly Linked Lists
* NodeJS

### Warmup <a id="warmup"></a>

* [Ajax-proxy](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week10/day04_ajax_proxy)

### Codealongs <a id="codealongs"></a>

* ​Singly Linked Lists​
* Node Servers

## Singly Linked List <a id="singly-linked-list"></a>

Singly Linked Lists are a type of data structure. In a singly linked list, each node in the list stores the contents and a pointer or reference to the next node in the list. It does not store any pointer or reference to the previous node. ... The last node in a single linked list points to nothing.

```bash
mkdir singly_linked_list
cd singly_linked_list/
touch singly_linked_list.rb
```

```ruby
class SinglyLinkedList
​
end
​
require 'pry'
binding.pry
```

```ruby
# add a class into the SinglyLinkedList Class
​
class SinglyLinkedList
​
  class Node
​
  end
​
end
```

```ruby
class SinglyLinkedList
​
  class Node
​
  end
​
  attr_accessor :head
​
  def initialize
    @head = nil
  end
​
end
```

```ruby
class SinglyLinkedList
​
  class Node
​
  end
​
  attr_accessor :head
​
  def initialize
    @head = nil
  end
​
  def prepend(value)
    node = Node.new(value)
    node.next = @head
    @head = node
  end
​
end
```

```ruby
class Node
  attr_accessor :value, :next
​
  def initialize(value)
    @value = value
    @next = nil
  end
end
```

Now we can run the program to see how it works.

```bash
ruby singly_linked_list.rb
```

Our `binging.pry`will keep us in the program as well will have access to the class.

```bash
pry(main)> SinglyLinkedList=> SinglyLinkedList
```

We are now able to instantiate a new instance of the `SinglyLinkedList`.

```bash
pry(main)> bros = SinglyLinkedList.new
=> #<SinglyLinkedList:0x00007fc048a83148 @head=nil>
```

We can then call the `prepend` method we just created to add a new node.

```bash
pry(main)> bros.prepend 'Groucho'
=> #<SinglyLinkedList::Node:0x00007fc0480c4d00 @next=nil, @value="Groucho">
```

This now have set the value of the head node to 'Groucho'.

```bash
pry(main)> bros
=> #<SinglyLinkedList:0x00007fc048a83148
 @head=#<SinglyLinkedList::Node:0x00007fc0480c4d00 @next=nil, @value="Groucho">>
​
pry(main)> bros.head
=> #<SinglyLinkedList::Node:0x00007fc0480c4d00 @next=nil, @value="Groucho">
​
pry(main)> bros.head.value
=> "Groucho"
```

Now if we were to add another Marx brother we will see that the head will change.

```bash
pry(main)> bros.prepend 'Harpo'
=> #<SinglyLinkedList::Node:0x00007fc0490d9880
 @next=#<SinglyLinkedList::Node:0x00007fc0480c4d00 @next=nil, @value="Groucho">,
 @value="Harpo">
​
pry(main)> bros
=> #<SinglyLinkedList:0x00007fc048a83148
 @head=
  #<SinglyLinkedList::Node:0x00007fc0490d9880
   @next=#<SinglyLinkedList::Node:0x00007fc0480c4d00 @next=nil, @value="Groucho">,
   @value="Harpo">>
​
pry(main)> bros.head.value
=> "Harpo"
```

We can see what the next head value or the previous node was.

```bash
pry(main)> bros.head.next.value
=> "Groucho"
```

As expected if you add another you can chain through to find the original node.

```bash
pry(main)> bros.prepend 'Zeppo'
=> #<SinglyLinkedList::Node:0x00007fc04806c218
 @next=
  #<SinglyLinkedList::Node:0x00007fc0490d9880
   @next=#<SinglyLinkedList::Node:0x00007fc0480c4d00 @next=nil, @value="Groucho">,
   @value="Harpo">,
 @value="Zeppo">
​
pry(main)> bros.head.value
=> "Zeppo"
​
pry(main)> bros.head.next.value
=> "Harpo"
​
pry(main)> bros.head.next.next.value
=> "Groucho"
```

```bash
def initialize(value=nil)
  @head = Node.new(value) if value
end
```

Make a method that finds the last node.

```bash
def last
  node = @head
  while node && node.next
    node = node.next # Traverse by one to the next node in the list.
  end
  node
end

```

We can now set a new instance of the class as the next node of the last.

```bash
def append(value) # AKA .push
  last.next = Node.new(value)
end
```

Run the program again.

```bash
ruby singly_linked_list.rb
​
​
    36: end
    37:
    38:
    39:
    40: require 'pry'
 => 41: binding.pry
```

Create a new instance of the class.

```bash
pry(main)> bros = SinglyLinkedList.new 'Groucho'
=> #<SinglyLinkedList:0x00007ffd690683f8
 @head=#<SinglyLinkedList::Node:0x00007ffd690683d0 @next=nil, @value="Groucho">>
​
pry(main)> bros.append 'harpo'
=> #<SinglyLinkedList::Node:0x00007ffd68ad62f0 @next=nil, @value="harpo">
​
pry(main)> bros.append 'chico'
=> #<SinglyLinkedList::Node:0x00007ffd68a85940 @next=nil, @value="chico">
​
pry(main)> bros.head.value
=> "Groucho"
​
pry(main)> bros.head.next
=> #<SinglyLinkedList::Node:0x00007ffd68ad62f0
 @next=#<SinglyLinkedList::Node:0x00007ffd68a85940 @next=nil, @value="chico">,
 @value="harpo">
```

## Node.js <a id="node-js"></a>

​[Node](https://nodejs.org/en/) is an open-source, cross-platform JavaScript engine that's mostly used to create web servers using JavaScript. It was written in 2009 by Ryan Dahl while he was working at Joyent.

### JavaScript engines​ <a id="javascript-engines"></a>

A JavaScript engine is a compiler that turns JavaScript into machine code for microprocessors - typically, it will turn it into things like:

* **IA32** - Intel Architecture 32 bit
* **x86-64** - A 64 bit version of the Intel Architecture
* **ARM** - Acorn Reduced Instruction Set Computing \(RISC\) Machine
* **MISP ISAs** - Microprocessor without Interlocked Pipeline Stages Instruction Set Architecture

​Here are a few JavaScript engines: ​

* **SpiderMonkey** - Firefox, Netscape Navigator - the first JavaScript Engine
* **V8** - Chrome, Opera
* **Chakra** - Internet Explorer
* **Nitro** - Safari

**Node** is the V8 JavaScript engine, taken out of a browser, with a little bit extra. It lets us write server-side code in JavaScript, allowing us to do the same sorts of things we do with Ruby.

## _NodeJS - JavaScript Engines - Further Reading_ <a id="nodejs-javascript-engines-further-reading"></a>

* ​[Wikipedia - JavaScript Engines](https://en.wikipedia.org/wiki/JavaScript_engine#JavaScript_engines)​

## Why NodeJS? <a id="why-nodejs"></a>

### _What is Node good at?_ <a id="what-is-node-good-at"></a>

* Streaming data
* "Soft" real-time
* Every developer knows a bit of JS
* "Tooling"
* Unopinionated and flexible
* It can be isomorphic
* Corporate backing
* Performant
* Good community - easy to find developers

### _What is Node not so good at?​_ <a id="what-is-node-not-so-good-at"></a>

* "Tooling" - too much out there
* Being opinionated
* Memory leaks
* Dependency injection
* Serving static files \(like HTML\)
* Providing structure
* Generic JavaScript woes \(callbacks, etc.\)
* Allowing easy debugging
* Producing light-weight codebases
* Providing functionality out of the box
* Getting away from fancy buzzwords

## Installation and Usage <a id="installation-and-usage"></a>

### _Installation_ <a id="installation"></a>

```bash
# Initial installation using Homebrew
brew install node
# Upgrading installed version using Homebrew
brew upgrade node
```

### _Usage_ <a id="usage"></a>

```bash
# Open a Node REPL
node
# Run a Node application
node someFileName.js
```

## _NPM - Introduction_ <a id="npm-introduction"></a>

### Usage <a id="usage-1"></a>

We haven't gotten into Webpack yet, but this is an example of how we would create a new NodeJS application.

### _Initialize an NPM project_ <a id="initialize-an-npm-project"></a>

Running this command will create a package.json file for your NodeJS application. This describes your application, and allows NPM to manage your application's dependencies.

```bash
npm init
```

We can also skip the 'wizard'-style Q&A process with the -y flag.

```bash
npm init -y
```

### _Install packages_ <a id="install-packages"></a>

This will install Webpack and all its dependencies. The --save flag will also add webpack to your package.json.

```bash
npm install webpack --save
```

### _Update packages_ <a id="update-packages"></a>

Periodically, you should update the packages on which your application depends. This will update all local packages in your package.json file \(and all their dependencies\).

```bash
npm update
```

### _Further Reading_ <a id="further-reading"></a>

* ​[NPM](https://www.npmjs.com/)​
* ​[NPM - Introduction](https://docs.npmjs.com/getting-started/what-is-npm)​
* ​[NodeSource - Understanding NPM](https://nodesource.com/)​
* ​[NPM Dependency Tree - Example: ExpressJS](http://npm.anvaka.com/#/view/2d/express)​

## Creating a simple Node server <a id="creating-a-simple-node-server"></a>

Create a new directory and cd into it then open in Atom.

```bash
mkdir simple-node-server
cd simple-node-server/
touch index.js
atom .
```

Add console log into the `index.js` file you've just created.

```javascript
console.log(`hello world`);
```

Run the program by using the below code in the terminal. Make sure you're in the `simple-node-server/` directory.

```bash
node index.js
```

You should be able to see the console log in the terminal `hello world.`

Go back to the `index.js` file and remove the console log as it was only used to make sure we have a connection. Define a variable and require 'http'

```javascript
const http = require('http');
```

Create a connection to the server with a 'fat arrow' function that way we can retain the value of `this`.

```javascript
http.createServer( (request, response) => {
​
});
```

This is a direct comparison of the old way of writing the function.

```javascript
http.createServer( function(request, response){
​
});
```

Because node is unopinionated we need to specify our requests and an end to the response.

```javascript
http.createServer( (request, response) => {
  response.writeHead(200, { 'Content-Type': 'test/plain' }); //telling browser this is not HTML its just plain text.
  response.end('Hello World');
});
```

We also have to tell the server to start with a 'listen' promise chained to the end of the function. This will watch port 8000.

```javascript
http.createServer( (request, response) => {
  response.writeHead(200, { 'Content-Type': 'test/plain' }); //telling browser this is not HTML its just plain text.
  response.end('Hello World');
}).listen(8000);
```

Unfortunately, Node doesn't log anything to the console so we have no way of knowing what's happening. We can get around this by placing console logs in our code.

```javascript
const http = require('http');
​
http.createServer( (request, response) => {
  response.writeHead(200, { 'Content-Type': 'test/plain' }); //telling browser this is not HTML its just plain text.
  response.end('Hello World');
}).listen(8000);
​
console.log('Server now running at http://localhost:8000');
```

Now go back to the terminal an run the server

```javascript
node index.js
```

Add some additional logs to let us know when someone is trying to request a page.

```javascript
http.createServer( (request, response) => {
  console.log( 'Page requested');
  response.writeHead(200, { 'Content-Type': 'test/plain' }); //telling browser this is not HTML its just plain text.
  response.end('Hello World');
}).listen(8000);
```

### Homework <a id="homework"></a>

*  Complete the Singly Linked List methods
* Node.js BA fake server:
  * make reservations & user\_reservations seat display work
  * make search results page work \(`/search/:origin/:destination`\), i.e. actually search through the `flights` array of objects and return the matching flights \(use `.filter()`\)
* YouTeach preparation, final project brainstorming
* MongoDB preview? [https://gist.github.com/nrollr/9f523ae17ecdbb50311980503409aeb3](https://gist.github.com/nrollr/9f523ae17ecdbb50311980503409aeb3)



### Further Reading <a id="further-reading-1"></a>

* ​[NodeJS](https://nodejs.org/docs/latest-v9.x/api/synopsis.html)​

###   <a id="further-reading"></a>

