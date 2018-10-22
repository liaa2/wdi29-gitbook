# Day 04

What we covered today:

* Emmet 
* JavaScript - Libraries
* JavaScript - jQuery - Introduction

### Slides <a id="slides"></a>

* ​[jQuery - Introduction​](https://github.com/textchimp/wdi-29/blob/master/week2/intro-to-jquery.pdf)

### Exercises <a id="exercises"></a>

1. ​[Making a Video Player](https://gist.github.com/textchimp/4871fa2c333cd19151db3ab8e0083513)​
2. ​[DOM Detective](https://gist.github.com/textchimp/00baa95feb73c773ac62c0547c3b3702)​

### Links <a id="links"></a>

​[Programmer Ryan Gosling](http://programmerryangosling.tumblr.com/)​

## Emmet

Emmet is an Atom Package for speeding up the process of coding HTML and CSS using **abbreviations** and **action shortcuts**. It's particularly helpful when writing HTML. Check out:

* ​[Emmet Cheat Sheet](http://docs.emmet.io/cheat-sheet/)​
* ​[Emmet Syntax](http://docs.emmet.io/abbreviations/syntax/)​

### Abbreviations <a id="abbreviations"></a>

All of Emmet's abbreviations work by writing the abbreviation and pressing tab at the end of the abbreviation.

#### _Tag Name_ <a id="tag-name"></a>

Whether it is a `p`, a `div`, or anything else. If you type the tag name, and then hit tab, it will create the element.

#### _Classes and IDs \( \# or . \)_ <a id="classes-and-ids-or"></a>

```markup
div.className
<!-- Makes: -->
< div class="className"></div>​

div#tagName
<!-- Makes: -->
<div id="tagName"></div>​

div.firstClassName.secondClassName
<!-- Makes: -->
<div class="firstClassName secondClassName"></div>

​div.className#secondClassName
<!-- Makes: -->
<div class="className" id="secondClassName"></div>
```

#### _Children \( &gt; \)_ <a id="children-greater-than"></a>

This is for nesting elements!

```markup
div>p
<!-- Makes: -->
<div>    
  <p></p>
</div>

​header>nav>p
<!-- Makes: -->
<header>    
  <nav>        
    <p></p>    
  </nav>
</header>
```

#### _Sibling \( + \)_ <a id="sibling"></a>

This is for creating elements next to each other.

```markup
header+div.container
<!-- Makes: -->
<header>
</header>
<div class="container">
</div>
```

#### _Multiplication \( \* \)_ <a id="multiplication"></a>

This is for making multiple elements at once.

```markup
div>ul>li*3
<!-- Makes: -->
<div>    
  <ul>        
    <li></li>        
    <li></li>        
    <li></li>    
  </ul>
</div>
```

#### _Climb Up \( ^ \)_ <a id="climb-up"></a>

This is to climb out of a nesting.

```markup
header>p^div
<!-- Makes: -->
<header>    
  <p></p>
</header>
<div></div>
```

#### _Grouping \( \(\) \)_ <a id="grouping"></a>

This is to group chunks of elements so you don't need to worry about climbing.

```markup
(header>h1)+(nav>a)
<!-- Makes: -->
<header>    
  <h1></h1>
</header>
<nav><a href=""></a></nav>
```

#### _Attributes \( \[\] \)_ <a id="attributes"></a>

This is to give custom attributes.

```markup
img[src="" title="" alt=""]
<!-- Makes: -->
<img src="" alt="" title="">
```

#### _Text \( {} \)_ <a id="text"></a>

This is to add text to things.

```markup
a{This is a link to something}
<!-- Makes: -->
<a href="">This is a link to something</a>
```

These things can all be used together!

```markup
div.container>(header>h1)+(ul>li*5)
<!--  Makes: -->
<div class="container">    
  <header>        
    <h1></h1>    
  </header>    
  <ul>        
    <li></li>        
    <li></li>        
    <li></li>        
    <li></li>        
    <li></li>    
  </ul>
</div>
```

### Action Shortcuts <a id="action-shortcuts"></a>

There are a bunch of these, but some particularly handy ones are:

* `cmd` + `up` - remove tag
* `ctrl` + `alt` + j - find matching tag
* `shift` + `cmd` + `m` - merge lines
* `cmd` + `shift` + `y` - evaluate maths expression
* `ctrl` + `d` - balance tags \(ie, select the tag boundaries from the current caret position\)

## JavaScript - Libraries <a id="javascript-libraries"></a>

### What is a library? <a id="what-is-a-library"></a>

A collection of reusable methods designed for a particular purpose. You just reference a javascript file with a particular library in it - and away you go!

jQuery is the most common JavaScript library on the web today. As of 2016, it was used in:

* Over 43 million websites, including:
  * Over 12% of all websites;
  * Over 78% of the top million websites;

## JavaScript - jQuery - Introduction <a id="javascript-jquery-introduction"></a>

#### _What is jQuery_ <a id="what-is-jquery"></a>

An open source JavaScript library that simplifies the interaction between HTML and JavaScript. A JavaScript library is collection of reusable methods for a particular purpose.

It was created by John Resig in 2005, and released in January of 2006.

Built in an attempt to simplify the existing DOM APIs and abstract away cross-browser issues.

#### _Why jQuery?_ <a id="why-jquery"></a>

* Well documented
* Lots of plugins
* Small-ish size \(23kb\)
* Everything works in IE 6+, Firefox 2+, Safari 3+, Chrome, and Opera 9+ \(if you are using 1.11.3 or previous, greater than that scraps up until IE8 support\)
* Millions and millions of sites using it.

#### _What does it do for us?_ <a id="what-does-it-do-for-us"></a>

* Data Manipulation
* DOM Manipulation
* Events
* AJAX
* Effects and Animation
* HTML Templating
* Widgets / Theming
* Graphics / Chart
* App Architecture

#### _Why use it?_ <a id="why-use-it"></a>

```javascript
// No library:
const elems = document.getElementsByTagName("img");
for (let i = 0; i< elems.length; i++) {  
  elems[i].style.display = "none";
}​

// jQuery:
$('img').hide();
```

> "The code that has the least amount of bugs is the code that doesn't exist." - _Joel Turnbull_

### The basics <a id="the-basics"></a>

**Select -&gt; Manipulate -&gt; Admire**

```javascript
const $paragraphs = $("p")
$paragraphs.addClass('special');​

// OR
$("p").addClass("special");
```

#### _Selecting elements_ <a id="selecting-elements"></a>

All CSS selectors are valid.

| HTML | CSS Selector | jQuery |
| :--- | :--- | :--- |
| `<p>` | `p` | `$('p')` |
| `<p class="intro">` | `.intro` | `$('.intro')` |
| _or_ | `p.intro` | `$('p.intro')` |
| `<p id="badger">` | `#badger` | `$('#badger')` |
| `<div> <p></p> </div>` | `div p` | `$('div p')` |
| `<ul> <li></li> <li></li> </ul>` | `ul li:last-child` | `$('ul li:last-child')` |

jQuery also offers a bunch of other selectors. Some common ones are:

| Selector | Example | Selects | ​ | ​ |
| :--- | :--- | :--- | :--- | :--- |
| `:first` | `$("p:first")` | The first paragraph element. | ​ | ​ |
| `:last` | `$("div > p:last")` | The last paragraph element that is a direct child of a div element | ​ | ​ |
| `:has()` | `$("div:has(img)")` | Any divs that have one or more descendent img elements | ​ | ​ |
| `:visible` | `$(".kitten:visible")` | Any elements with the class "kitten" that have height | ​ | width &gt; 0 |
| `:hidden` | `$(".kitten:hidden")` | The opposite of :visible. Includes `display:none`. | ​ | ​ |

See [jQuery API - Selectors](http://api.jquery.com/category/selectors/).

#### _Reading elements_ <a id="reading-elements"></a>

If we had this element in the HTML...

`<a id="yahoo" href="http://www.yahoo.com" style="font-size:20px">Yahoo!</a>`

We can select it using `$("a#yahoo")`

We can store it using `let $myLink = $("#yahoo");`

We can get the content within it using `$("#yahoo").html()`

We can get the text within it using `$("#yahoo").text()`

We can get the HREF attribute using `$("#yahoo").attr("href")`

We can get the CSS attribute using `$("#yahoo").css('font-size')`

#### _Changing elements_ <a id="changing-elements"></a>

`$("#yahoo").attr("href", "http://generalassemb.ly")`

`$("#yahoo").css("font-size", "25px")`

`$("#yahoo").text("General Assembly")`

`$("#yahoo").attr("href", "http://generalassemb.ly").css("font-size", "25px").text("General Assembly")`

#### _Create, manipulate and inject_ <a id="create-manipulate-and-inject"></a>

```javascript
// Step 1: Create element and store a reference    
const $para = $('<p></p>'); // You can create any element with this!​

// Step 2: Use a method to manipulate (optional)    
$para.addClass('special'); // So many functions you could use

​// Step 3: Inject into your HTML    
$('body').append($para); // Also could use prepend, prependTo or appendTo as well
```

### HTML elements v DOM nodes v jQuery objects <a id="html-elements-v-dom-nodes-v-jquery-objects"></a>

A DOM node is not actually an HTML element - it is a representation of an HTML element, which we can use to create, modify, and read properties of HTML elements.

Similarly, it's important to note that a jQuery object is not actually a DOM node - it is a wrapper around a DOM element/collection of DOM elements that allows us to use the jQuery library's methods.

Consider this HTML:

```markup
<div>  
  <p> This is a paragraph of text.</p>
</div>
```

We can't access and interact with an HTML element directly from JavaScript.

```javascript
<p>
// => Uncaught SyntaxError: Unexpected token <
```

We need to use the DOM API to select the DOM node that represents that HTML element.

```javascript
document.querySelector("p");
// => <p> This is a paragraph of text.</p>
```

This is a DOM node, not an HTML element.

```javascript
typeof(document.querySelector("p"));
// => "object"
```

If we create a jQuery object but want to access the DOM elements within that object, we need to pull out the native DOM element from the jQuery object.

```javascript
let paragraph = document.querySelector("p");  
// This is a DOM node.
let $paragraph = $("p:first");                
// This is a jQuery element.

​$paragraph === paragraph
// => false
// The first object is a jQuery object. The second object is a DOM node.

​$paragraph;
// => [ <p> This is a paragraph of text </p> ]
// Note the square brackets - this is a jQuery object, not a DOM node.

​let p = paragraph[0]
// We have taken the jQuery object and stored the first DOM node in that element to 
//a variable called p

​p === paragraph
// => true
```

While we can mix regular JavaScript and jQuery together in our code, we cannot call jQuery methods on regular DOM objects \(and vice-versa\).

```javascript
// CREATING A JQUERY OBJECT

​let $paragraphs = $('p');
// This creates an array-like jQuery object comprised of all the DOM elements in the 
//Document Object Model that represent paragraph tags.​

// GETTING A DOM NODE FROM A JQUERY OBJECT - METHOD 1​
let firstParagraph = $paragraphs[0];
// This is a DOM node. We have selected the first DOM node in the $paragraphs jQuery 
//object​

// GETTING A DOM NODE FROM A JQUERY OBJECT - METHOD 2​
let firstParagraph = $paragraphs.get(0);
// This is a DOM node. We have selected the first DOM node in the $paragraphs jQuery 
//object using jQuery's .get() method.

​let allParagraphs = $paragraphs.get();
// This is an array DOM nodes. We have created 
//an array of all the native DOM nodes in the $paragraphs jQuery object using 
//jQuery's .get() method without passing any arguments.​

// CREATING A JQUERY OBJECT FROM ANOTHER JQUERY OBJECT​
let $myParagraph = $( paragraphs[0] );
// This is a jQuery object.

​let $myParagraph = $paragraphs.el(0);
// This is a jQuery object - this is the preferred method.

​// We can also loop through our array...
for( let i = 0; i < paragraphs.length; i++ ) {   
  let element = paragraphs[i];   
  let paragraph = $(element);   
  paragraph.html(paragraph.html() + ' wowee!!!!');
};​

// Or use jQuery to do it - this is preferred
$paragraphs.each(function () {  
  let $this = $( this );  
  $this.html( $this.html() + " wowee!!!" );
});
```

\_\_

## Homework <a id="homework"></a>

* ​[The Cat Walk - do it in jQuery](https://gist.github.com/wofockham/b4a62f016bfd241627dd)

[  
](https://granthanrahan.gitbook.io/wdi27/daily-stuff/week-02/day-03/javascript-animation/callbacks)

