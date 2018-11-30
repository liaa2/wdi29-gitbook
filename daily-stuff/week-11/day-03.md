# Day 03

What we covered today:

* Regular expressions
* Node.js Testing

### Warmup <a id="warmup"></a>

* [Text Soup 3](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week11/day03_textsoup3)

### Codealongs <a id="codealongs"></a>

* ​regular-expressions​
* [​node-testing-jasmine​](https://github.com/textchimp/wdi-29/tree/master/week10/node-servers/ba-express-server-mongodb)

## Regular Expressions I <a id="regular-expressions-i"></a>

Regular Expressions are pattern matchers for text. Sounds relatively dry \(or very, very dry\) but they are incredibly powerful. They are often considered a write-only language. You can write it, but it is virtually impossible to read. They occur in lots and lots of programming languages \(they are even in javascript\), and if you are interested in the history of them - see [here](https://en.wikipedia.org/?title=Regular_expression#History) - but the way that Ruby works with them stems from the Perl programming language.

### So, how do we work with them in Ruby? <a id="so-how-do-we-work-with-them-in-ruby"></a>

#### _Literal Characters_ <a id="literal-characters"></a>

We can match literal characters in virtually the same way as we would with two equals signs. Instead of using the two equals signs though, we use `=~` , think of this as a fuzzy or dynamic search. To specify a regular expression in Ruby \(and most other languages\), we use `//` \(these are considered Regexp delimiters\). Let's have a muck around with them.

```ruby
"bob" == "bob" # This obviously returns true.
​
"bob" =~ /bob/
# This is true, they do match. But instead of returning true, it returns the index of where the pattern started to match. In this case, it returns 0.  It returns nil if it doesn't match anything.
​
"Hello, my name is bob" =~ /bob/
# Again, this is true, but returns 18
```

Obviously this isn't the powerful part though, considering this does virtually the same thing as the multiple equals signs. So let's get into some of the cooler stuff.

#### _Metacharacters_ <a id="metacharacters"></a>

In regular expressions, there are characters that mean far more than literal characters. This can prove problematic \(but there are ways to escape metacharacters\), but also the source of some of the most powerful parts.

```ruby
"o!o" =~ /o.o/ # Returns 0
```

#### _Character Classes_ <a id="character-classes"></a>

These are often used to check for capitalized and uncapitalized versions, but can also be used to check for multiple letters. The metacharacters for these are `[]`.

```javascript
"bob" =~ /[Bb]ob/  # Returns 0
"Bob" =~ /[Bb]ob/  # Returns 0
"cob" =~ /[Bbc]ob/ # Returns 0
"dog" =~ /[Bb]ob/  # Returns nil
"any vowels" =~ /[aeiou]/ # Returns 0
```

For this sort of stuff, we can also use ranges. These are quite useful.

```javascript
"A" =~ /[A-Z]/      # Returns 0
"a" =~ /[A-Z]/      # Returns nil
"a" =~ /[A-z]/      # Returns 0
```

There are lots of inbuilt ranges, and these are really useful to know. Some of them are...

* `\s` - Will match any space characters \(spaces, new lines etc.\)
* `\S` - Anything other than space characters
* `\w` - Will match any word character \(i.e. actual letters or numbers\)
* `\W` - Will match any non-word character

```ruby
"Wolf" =~ /[\w]/    # Returns 0
"Wolf" =~ /[\W]/    # Returns nil
"Wolf " =~ /[\W]/   # Returns 4
​
"Wolf " =~ /[\s]/   # Returns 4
"Wolf " =~ /[\S]/   # Returns 0
```

We can obviously add lots and lots of things between those square brackets. But there are other ways we can do this as well. We can use `()` and `|` to check for multiple things.

```ruby
"Jane" =~ /(Jane|Serge)/    # Returns 0
"Serge" =~ /(Jane|Serge)/   # Returns 0
```

The round brackets are metacharacters in Regexp as well! They are a way to say this or this \(or this or this or this\). The pipe is the delimiter for saying "or".

There are a lot more metacharacters. The `.`, for example, is a wildcard, it will match anything.

```ruby
"jane" =~ /.ane/            # Returns 0
"zane" =~ /.ane/            # Returns 0
"Serge and Jane" =~ /.ane/  # Returns 10
```

This is still relatively hardcoded though, we need to specify where the characters are and what they are. To help solve this problem, there are quantifiers.

#### _Quantifiers_ <a id="quantifiers"></a>

Quantifiers are a way to check in Regexp whether things exist, or exist more than once etc.

The ones that you will actually use:

* `+` means one or more
* `?` means one or zero
* `*` means zero or more

It can look like the following:

```ruby
"Hi there" =~ /i+/      # Returns 1
"Hi there" =~ /the?/    # Returns 3
"Hi theeere" =~ /the*/  # Returns 3
```

These are regularly used for existence checks.

#### _Capturers_ <a id="capturers"></a>

These are difficult to understand. Basically, you match something in parentheses and can refer back to them. You capture something by using round brackets, and refer back to them using a `\` and an integer \(that mimics the order of capture\).

```ruby
"WolfWolf" =~ /(....)\1/
# Matches any four characters, but then needs to have the same four characters straight after.  This returns zero.
​
"ArcticWolf ArcticWolf" =~ /(......)(....) \1\2/
# Matches "Arctic" in the first brackets, then "Wolf" in the second brackets.  "Arctic" is saved as \1 and "Wolf" is saved as \2
```

#### _Regex Cheatsheet_ <a id="regex-cheatsheet"></a>

* ​[Cheatsheet](https://www.ralfebert.de/snippets/ruby-rails/regex_cheat_sheet/)​

## Testing in Node <a id="testing-in-node"></a>

Testing is a key element to any application. For Node.js, a Framework available for Testing is called Jasmine. Jasmine was initially known as JsUnit before being upgraded and renamed.

Jasmine helps in automated Unit Testing, something which has become quite a key practice when developing and deploying modern day web applications.

### _Overview of Jasmine for testing Node.js applications_ <a id="overview-of-jasmine-for-testing-node-js-applications"></a>

Jasmine is a **Behavior Driven Development\(BDD\)** testing framework for JavaScript. It does not rely on browsers, DOM, or any JavaScript framework. Thus, it's suited for websites, Node.js projects, or anywhere that JavaScript can run. To start using Jasmine, you need to first download and install the necessary Jasmine modules.

Next you would need to initialize your environment and inspect the jasmine configuration file. The below steps show how to setup Jasmine in your environment

**Step 1\)** Installing the NPM Modules

To use the jasmine framework from within a Node application, the jasmine module needs to be installed first. To install the jasmine-node module, run the below command.

```bash
npm install --save-dev jasmine request 
```

**Step 2\)** Initializing the project – By doing this, jasmine creates a spec directory and configuration json for you. The spec directory is used to store all your test files. By doing this, jasmine will know where all your tests are, and then can execute them accordingly. The JSON file is used to store specific configuration information about jasmine.

To initialize the jasmine environment, run the below command

```bash
./node_modules/.bin/jasmine init
```

**Step 3\)** Inspect your configuration file. The configuration file will be stored in the spec/support folder as jasmine.json. This file enumerates the source files and spec files you would like the Jasmine runner to include.

```javascript
{
  "spec_dir": "spec",
  "spec_files": [
    "**/*[sS]pec.js"
  ],
  "helpers": [
    "helpers/**/*.js"
  ],
  "stopSpecOnExpectationFailure": true,
  "random": false
}

```

### _Using Jasmine to test Node.js applications_ <a id="using-jasmine-to-test-node-js-applications"></a>

In order to use Jasmine to test Node.js applications, a series of steps needs to be followed.

In the example below, we are going to define a module which add 2 numbers which need to be tested. We will then define a separate code file with the test code and then use jasmine to test the Add function accordingly.

**Step 1\)** Define the code which needs to be tested. We are going to define a function which will add 2 numbers and return the result. This code is going to be written in a file called `Add.js.`

```javascript
// The "exports" keyword is used to ensure that the functionality defined in this file can actually be accessed by other files.
var exports = module.exports = {};
​
// We are then defining a function called 'AddNumber.' This function is defined to take 2 parameters, a and b. The function is added to the module "exports" to make the function as a public function that can be accessed by other application modules.
exports.AddNumber = function( a,b ){
  // We are finally making our function return the added value of the parameters.
  return a+b;
};
```

**Step 2\)** Next we need to define our jasmine test code which will be used to test our "Add" function In the Add.js file. The below code needs to put in a file called add-spec.js.

_Note:_ - The word 'spec' needs to be added to the test file so that it can be detected by jasmine.

```javascript
// We need to first include our Add.js file so that we can test the 'AddNumber' function in this file.
var app = require("../Add.js");
​
// We are now creating our test module. The first part of the test module is to describe a method which basically gives a name for our test. In this case, the name of our test is "Addition".
describe("Addition",function(){
  // The next bit is to give a description for our test using the 'it' method.
  it("The function should add 2 numbers",function() {
    // We now invoke our Addnumber method and send in 2 parameters 5 and 6. This will be passed to our Addnumber method in the App.js file. The return value is then stored in a variable called value.
    var value = app.AddNumber(5,6);
    // The final step is to do the comparison or our actual test. Since we expect the value returned by the Addnumber function to be 11, we define this using the method expect(value).toBe(the expected value).
    expect(value).toBe(11);
  });
});
```

In order to run the test, run the command `jasmine`.

### _Automated testing with Nodemon_ <a id="automated-testing-with-nodemon"></a>

Nodemon can be used to automate the tests so that you do not need to run `npm run test` each time.

In package.json add the following `"watch"` script

```javascript
  "scripts": {
    "test": "jasmine || true",
    "watch": "nodemon --exec jasmine",
    "seed": "mongoimport --db ba --collection flights --drop --jsonArray --file seeds-flights.js",
    "server": "nodemon server.js",
    "debug": "ndb npm run server"
  },
```

Now the tests can be run with the command `npm run watch`

### \_\_

### _Further Reading_

* ​[Using Jasmine to test Node.js Applications](https://blog.codeship.com/jasmine-node-js-application-testing-tutorial/)​
* ​[Jasmine](https://jasmine.github.io/)​
* ​[THE Regular Expression book](http://shop.oreilly.com/product/9780596528126.do)​
  * ​[Good Regexp chapters:](http://shop.oreilly.com/product/0636920018452.do)​
* ​[Regexp in Ruby](http://ruby-doc.org/core-2.1.1/Regexp.html)​
* ​[RegExp in JS](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)​
* ​[Test regular expressions interactively:](http://rubular.com/)​
* ​[Regex Crossword](https://regexcrossword.com/)​



