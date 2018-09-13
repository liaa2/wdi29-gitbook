# Day 04

What we covered today:

* ​[Warmup and solution - Serge - JS​](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week01/day04_sergeSays)
* Review [Shakespeare insult generator​](https://github.com/textchimp/wdi-29/tree/master/week1/insult-generator)
* JavaScript - Objects

### Slides {#slides}

* ​[Javascript Objects​](https://textchimp.github.io/wdi-29/week1/javascript-collections.pdf) \(slide 19 onwards\)

### Classwork {#classwork}

* ​[Shakespeare insult generator​](https://github.com/textchimp/wdi-29/tree/master/week1/insult-generator)
* ​[Week 1 Exercises​](https://github.com/textchimp/wdi-29/tree/master/week1)

## JavaScript - Collections - Objects {#javascript-collections-objects}

In JavaScript, an object is a standalone entity - filled with properties and types \(or keys and values\). It is very similar in structure to a dictionary.

So, most javascript objects will have keys and values attached to them - this could be considered as a variable that is attached to the object \(also allows us to iterate through them\).

They are sometimes called "associative arrays". Remember that they are not stored in any particular order \(they can change order whenever\).

### How to create an object {#how-to-create-an-object}

```javascript
// With object literal
const newObject = {};

​// Using Object
const newObject = new Object();
```

### How to add properties to an object {#how-to-add-properties-to-an-object}

```javascript
// Remember to seperate by commas!
const newObject = {  
    objectKey: "Object Value",  
    anotherObjectKey: "Another Object Value",  
    objectFunction: function () {​ 
     
    }
};​

const newObject = {};
newObject.objectKey = "Object Value";
newObject.objectFunction();
newObject["anotherObjectKey"] = "Another Object Value";​

// Can also use Constructors and Factories - will see them in Week 1 Day 5 notes.
```

### How to access properties of an object {#how-to-access-properties-of-an-object}

There are two ways to access the properties of an object:

* **Dot notation** - syntax: `object.propertyName`
* **Square bracket notation** - `object["propertyName"]`

Remember: like all JS variables - both the object name and property names are case sensitive.

```javascript
const favouriteCar = {  
    manufacturer: "Jaguar",  
    year: 1963,  
    model: "E-Type"
}​

// Dot notation access to object properties
favouriteCar.year​

// Square bracket notation access to object properties
favouriteCar["year"]

//however, if we create a new variable 
const key = "year"
key 
//=> "year"
//if we run the code via dot notation
favouriteCar.key //=> undefined
// via breacket(array-style) notation
favouriteCar[key] //=> 1963

//the things inside [] get evaluated
```

* ​[Objects: Exercises](https://gist.github.com/textchimp/23db045edf474762828a9e912912c873)​

### How to iterate through an object {#how-to-iterate-through-an-object}

```javascript
Object.keys(newObject); // Returns an array of all the keys in the specified object.
Object.getOwnPropertyNames(newObject); // So does this

​const obj = {  
    a: 1,  
    b: 2,  
    c: 3
};​

//we use bracket notation to get value
for (let key in obj) {  
    console.log( `key: ${key}, value: ${obj[key]}`);
}
// key: a, value: 1
// key: b, value: 2
// key: c, value: 3

//however, for dot notation
for (let key in obj) {  
    console.log( `key: ${key}, value: ${obj.key}`);
}
// key: a, value: undefined
// key: b, value: undefined
// key: c, value: undefined

//if using dot notatin, it will literally looking for the key called "key".
```

### Deleting properties of an object {#deleting-properties-of-an-object}

```javascript
const favouriteCar = {  
    manufacturer: "Jaguar",  
    year: 1963,  
    model: "E-Type"
}​

delete favouriteCar.year;
favouriteCar
//=>  { manufacturer: "Jaguar", model: "E-Type"}​    
```

### Comparing objects {#comparing-objects}

In JavaScript objects are a reference type. Two distinct objects are never equal, even if they have the same properties. Only comparing the same object reference with itself yields true.

```javascript
// Two variables, two distict objects with the same properties
const fruit = { name: "apple" };
const fruitbear = { name: "apple" };

​fruit == fruitbear;
// => false
fruit === fruitbear;
// => false​

// Two variables, a single object
const fruit = { name: "apple" };
const fruitbear = fruit;  // Assigns fruit object reference to fruitbear

​// Here fruit and fruitbear are pointing to same object
fruit == fruitbear;
// => true
fruit === fruitbear;
// => true
```

There's no simple way to compare objects using 'vanilla' JavaScript, but there are some JavaScript libraries that make object comparison easier - UnderscoreJS, for example, has an method - "\_.isEqual", which tests equality based on object properties. There are lots of alternatives - for example, check out [this](http://stackoverflow.com/questions/1068834/object-comparison-in-javascript) Stack Overflow thread - but I would stick to Underscore's method. [Underscore](http://underscorejs.org/) is a great JavaScript library which we'll be talking about it in great detail later on.

\_\_

## Homework {#homework}

* ​[Javascript Bank](https://gist.github.com/textchimp/be5cff64c320d0e0aa3008db0f3bfe85)​
* Bonus - Read:
  * ​[MDN - Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) - MDN is an amazing resource for JavaScript, HTML and CSS.
  * ​[JavaScript Tutorials - Arrays](http://javascript.info/tutorial/array)​
  * ​[Speaking JavaScript - Arrays](http://speakingjs.com/es5/ch01.html#basic_arrays)​

