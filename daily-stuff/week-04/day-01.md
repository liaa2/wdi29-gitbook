# Day 01

What we covered today:

* Ruby - Installation and RVM
* Ruby - A Brief History of Ruby
* Ruby - Introduction
  * Data Types
    * Strings and Numbers
  * Operators
  * Variables
  * Methods
  * Ruby - Fundamentals - Part I
  * Conditionals
  * Control Structures
* Ruby - Methods
* Ruby - Collections
  * Arrays
  * Hashes
* Ruby Basics Part II
* ​[Guest Speaker: Taryn Ewens - slides](https://docs.google.com/presentation/d/1OK_ZfmdIVS-cKkP4cqjCbK7-6vPGtnPgtLY5bbeWfvU/edit?usp=sharing)

### Slides <a id="slides"></a>

* ​[Ruby - Introduction​](https://github.com/textchimp/wdi-29/blob/master/week4/introduction-to-ruby.pdf)
* [Collections​](https://github.com/textchimp/wdi-29/blob/master/week4/collections-in-ruby.pdf)

## Ruby - Installation and RVM <a id="ruby-installation-and-rvm"></a>

* ​[RVM and Ruby Installation Guide](https://gist.github.com/ga-wolf/98718aa5c63d8323ae46)​

### How to get Ruby <a id="how-to-get-ruby"></a>

Install Developer Tools from Xcode \(this should have happened for most of you\):

`xcode-select --install`

Install HomeBrew:

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Access a specific URL using a secured line and run the downloaded program:

`curl -sSL https://get.rvm.io | bash -s stable`

Restart the terminal, and try running the command:

`rvm`.

If it doesn't work...

* Open the bash\_profile up in Atom

  `atom ~/.bash_profile`

* Add these lines into the bottom of the .bash\_profile and save it

  `[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"`

  `export PATH="$PATH:$HOME/.rvm/bin"`

Restart the terminal and run the following commands to make sure it's all cool:

`rvm`

`rvm list known`

`rvm get stable --auto`

Go here and find the most recent version - [https://www.ruby-lang.org/en/downloads/](https://www.ruby-lang.org/en/downloads/)​

Latest version at the time of writing was 2.4.0, swap those in for the latest stable version that shows on that website

`rvm install ruby-2.4.0`

`rvm --default use 2.4.0`

Let's test that it has all worked.

* `ruby -v`
* `rvm -v`
* `which ruby` - should not return anything in the /usr/local/bin
* `which rvm`

If all of this has worked, run...

`gem install pry`

### Common Commands <a id="common-commands"></a>

`ruby -v` - Will return the current version of Ruby

`which ruby` - What is the path to the version of Ruby you are using

`ruby hello_world.rb` - Runs the hello\_world.rb file

`irb` - Runs a ruby console

`pry` - Runs a better console

`<CTRL> + D` - Ends a file running in irb or ruby

## Ruby - A Brief History of Ruby <a id="ruby-a-brief-history-of-ruby"></a>

Created in 1993 by Yukihiro Matsumoto \(Matz\). He knew Perl and he also knew Python. He thought that Perl smelt like a toy language apparently, and he disliked Python because it wasn't a true object-oriented programming language. Ruby was primarily influenced by Perl and SmallTalk though.

Matz wanted a language that:

* Syntactically Simple
* Truly Object-Oriented
* Had Iterators and Closures
* Exception Handling
* Garbage Collection
* Portable

### Programming Mottos <a id="programming-mottos"></a>

* Perl - There's More Than One Way To Do It \(T.M.T.O.W.T.D.I\)
* Python - There Should Be One And Only One Way To Do It
* Ruby - Designed For Programmer Happiness

### _Further Reading - A Brief History of Ruby_ <a id="further-reading-a-brief-history-of-ruby"></a>

* ​[SitePoint - History of Ruby](http://www.sitepoint.com/history-ruby/)​

## Ruby - Introduction <a id="ruby-introduction"></a>

### Data Types - Strings and Numbers <a id="data-types-strings-and-numbers"></a>

#### _Strings_ <a id="strings"></a>

Again, delimited by quotes.

`"string"` `'string'`

#### _Numbers_ <a id="numbers"></a>

There are multiple types:

* FixNum
* Float
* BigNum

### Operators <a id="operators"></a>

#### _Arithmetic Operators_ <a id="arithmetic-operators"></a>

Lots of them, but the basic ones are:

```ruby
+     # Addition
-     # Subtraction
*     # Multiplication
/     # Division
**    # Exponent (to the power of)
%     # Modulus
```

#### _Assignment Operators_ <a id="assignment-operators"></a>

```ruby
=     # Assignment
+=    # Add then assign
-=    # Subtract then assign
*=    # Multiply then assign
/=    # Divide then assign
%=    # Modulus then assign - assigns the remainder of the modules to the left 
      #operand
```

#### _Logical Operators_ <a id="logical-operators"></a>

```ruby
&&    # And
and   # And (alternative to &&)
||    # Or
or    # Or (alternative to ||)
!     # Not
not   # Not (alternative to !)
```

#### _Comparison Operators_ <a id="comparison-operators"></a>

All the usual suspects, plus a few new ones:

```text
>       # Greater than
>=      # Greater than or equal to
<       # Less than
<=      # Less than or equal to
==      # Equality (generally just use the double equals in Ruby)
!=      # Inequality
<=>     # Combined comparison - returns -1 if less than, 0 if equal, and 1 if greater 
        #than
.eql?   # True if the receiver and argument have the same type and equal values
.equal? # True if the receiver and the argument have the same object ID
```

### _Ruby - Operators - Recommended Readings_ <a id="ruby-operators-recommended-readings"></a>

* ​[Tutorials Point - Ruby Operators](https://www.tutorialspoint.com/ruby/ruby_operators.htm)​

### Variables <a id="variables"></a>

Unlike JavaScript, we don't need to use the `let` or `const` \(or any other\) keyword when declaring a variable in Ruby.

`ruby = "is nice"`

It's much harder to accidentally make global variables in Ruby.

`$ruby = "is nice"`

To make a `const` variable you must define the variable name ALL in caps.

`RUBY = "is nice"`

Ruby will allow you to change this constant variable but will notify you if you change it.

### Methods \(Functions in JS\) <a id="methods-functions-in-js"></a>

`puts "this is like console.log` 

`print "this is also like console.log`

 `p "this is a bit more complex`

Parentheses in method calls are mostly optional in Ruby, but they are occasionally necessary \(eg, in method or function chaining\)

```text
puts("this")
puts "is the same as this"
```

Methods in Ruby have an **implicit return**, meaning that you don't need to use the `return` keyword in your methods - Ruby returns the last statement in a method on its own.

## Ruby Fundamentals - Pt I <a id="ruby-fundamentals-pt-i"></a>

#### _Basic naming conventions_ <a id="basic-naming-conventions"></a>

snake\_case\_everywhere - it's very rare to see camelCase!

#### _Variable interpolation in strings_ <a id="variable-interpolation-in-strings"></a>

String interpolation is where we put Ruby code to be evaluated inside a string - the code to be evaluated is inserted within `#{}`. This is most often used when interpolating variables, but we can put any expression within the curly brackets \(eg `#{5 + 4}` will interpolate `9` into the string\).

```ruby
name  = "gilberto"
drink = "scotch"

​"My name is #{ name } and I drink #{ drink }!"
# A lot nicer than "my name is " + name + " and I drink " + drink
# Which is the way you would do it in JS
```

IMPORTANT: Interpolation only works with double quotes!! Single quotes mean 'leave this string alone, this is mine'.

#### _Comments in Ruby_ <a id="comments-in-ruby"></a>

```ruby
# This is is a single line comment​
# This is
# a multiline
# comment​

# OR (don't do this)​

=begin
This is also a multi line comment
You can't have any an empty line between the =begin and the start of the comment
=end
```

#### _Getting user input_ <a id="getting-user-input"></a>

In JavaScript, we have `alert` and `prompt`, in Ruby we have `puts` and `gets`.

```ruby
# Initial greeting
puts "What is your first name?"​

# first_name = gets
# This will wait for user input, and include the new line in the variable

​first_name = gets.chomp
# This will wait for user input, and strip the new line from the variable
# For more documentation on chomp:
# http://ruby-doc.org/core-2.2.0/String.html#method-i-chomp

​puts "Your first name is #{ first_name }."

​p "What is your surname? " # using `p` will allow you to put the input on the same 
#line.
surname = gets.chomp # Chaining

puts "Your surname is #{ surname }."​
puts "Your full name is #{ first_name } #{ surname }"
# fullname = "#{ first_name } #{ surname }"
# Sames as ... puts "Your full name is #{ fullname }"

​puts "What is your address?"
address = gets.chomp
puts "Your name is #{ fullname } and you live at #{ address }"

​# INTERPOLATION ONLY WORKS IN DOUBLE QUOTES!
```

### Conditionals <a id="conditionals"></a>

#### `If` _statements_ <a id="if-statements"></a>

```text
if 13 > 10    
  p "Yep, it is a bigger number"
end​

grade = "A"

​if grade == 'A'    
  puts "You are killing it"
elsif grade == 'B'    
  puts "You are coasting fine"
elsif grade == 'C'    
  puts "Acceptable"
else    
  puts "Please see me after class"
end​

p "Yep, it is a bigger number" if 13 > 10 # This only works in single line statements​

# It's called a modifier (if modifier)
```

#### `Unless` _statements_ <a id="unless-statements"></a>

```ruby
x = 1
unless x > 2    
  puts "x is less than 2"
else    
  puts "x is greater than 2"
end

​# Modifier or backwards form
code_to_perform unless conditional
```

#### `case` _statements_ <a id="case-statements"></a>

Think of these as shorter if statements, but don't overuse them \(particularly in JS\)

```ruby
grade = 'B'
case grade
when 'A'    
  p 'You are killing it'
when 'B'    
  p 'You are coasting fine'
when 'C'    
  p 'Acceptable'
else    
  p 'Please see me after class'
end​

case expression_one
when expression_two, expression_three    
  statement_one
when expression_four, expression_five    
  statement_two
else    
  statement_three
end

​# Very similar to the switch statement in JavaScript!
```

The case statement will compare the **case expression** with whatever a particular **when expression** evaluates to. This is fine when testing direct equality between the case expression and the when expressions. Example:

```ruby
score = 1
case score
when 1  
  print "You got one"
when 2  
  print "You got two"
end
# => "You got one"
```

The first `when` expression - `1` - evaluates to `1`, and since `1 == 1` evaluates to `true`, the first `when` expression is satisfied, and "You got one" is printed

But this is a problem when our `when` expression contain is more complex. Consider the following:

```ruby
score = 1
case score
when score <= 1  
  print "You got one or less"
when score > 1  
  print "You got two or more"
end
# => nil
```

The first `when` expression - `score <= 1` - evaluates to `true`, and since `1 != true`, so none of the `when` expressions will be satisfied.

For complex expressions, the case expression should be left blank.

```text
score = 1
case
when score <= 1  
  print "You got one or less"
when score > 1  
  print "You got two or more"
end
# => "You got two or more"
```

### _Ruby - Conditionals - Exercises_ <a id="ruby-conditionals-exercises"></a>

* ​[Drinking Age, Air Conditioning, Sydney Suburbs​](https://gist.github.com/textchimp/0065f9596b90cd977b003594b9b7834b)
* ​ [Solution​](https://github.com/textchimp/wdi-29/tree/master/week4/ruby-conditionals-exercises)

### Control Structures <a id="control-structures"></a>

#### _While Loops_ <a id="while-loops"></a>

```text
while conditonal    
  statement
end

​while true    
  p "OMG"
end # BAD IDEA​

i = 0
while i < 5    
  puts "i: #{ i }"    
  i += 1
end
```

#### _Until Loops_ <a id="until-loops"></a>

```text
until conditional    
  statement
end​

i = 0
until i == 5    
  puts "i: #{ i }"    
  i += 1
end
```

#### _Iterators_ <a id="iterators"></a>

So, so common in Ruby.

```ruby
5.times do    
  puts "OMG"
end
# => OMG
# => OMG
# => OMG
# => OMG
# => OMG

​5.times do |i|    
  puts "I: #{ i }"
end
# => I: 0
# => I: 1
# => I: 2
# => I: 3
# => I: 4
# => I: 5

​​5.downto(0) do |i|    
  puts "I: #{ i }"
end
# => I: 5
# => I: 4
# => I: 3
# => I: 2
# => I: 1
# => I: 0
```

#### `for` _loops_ <a id="for-loops"></a>

**For loops** are very rarely used in Ruby.

```ruby
# Don't ever use them
for i in 0..5   
  puts "I: #{ i }"
end
# => I: 0
# => I: 1
# => I: 2
# => I: 3
# => I: 4
# => I: 5
```

#### _Generating random numbers_ <a id="generating-random-numbers"></a>

```ruby
Random.rand # Generates a number between 0 and 1
Random.rand(10) # Generates a random number up to 10 (including zero and 10)
Random.rand(5..10) # Generates a number between 5 and 10 (also includes them)
Random.rand(5...10) # Does not include 5 and 10
```

### _Ruby - Control Structures - Exercise_ <a id="ruby-control-structures-exercise"></a>

* [​Guess The Number​](https://gist.github.com/textchimp/391d14a59080a8b35c4262ec113d2f7e)
* ​[Solution​](https://github.com/textchimp/wdi-29/tree/master/week4/guessing-game)

## Methods <a id="methods"></a>

Methods are declared using the `def` keyword and called using the method's name.

### Methods with no arguments <a id="methods-with-no-arguments"></a>

```ruby
# Method definition
def hello    
  puts "Hello"
end​

# Method call
hello
# => "Hello"
```

### Methods with arguments <a id="methods-with-arguments"></a>

For methods with defined parameters, arguments can be passed in with or without parentheses.

```ruby
def hello( name )    
  puts "Hello, #{name}"
end​

hello("Grant")
# => "Hello, Grant"

​hello "Grant"
# => "Hello, Grant"
```

If a method is defined with one or more parameters but is called without passing in the right number of arguments, an error will be thrown \(`Argument Error: wrong number of arguments`\).

### Methods with default arguments <a id="methods-with-default-arguments"></a>

To avoid `Argument Error`s thrown by calling an argument without the requisite number of arguments, we can set default parameters in the method definition.

```ruby
def hello( name = "World" )  
  puts "Hello, #{name}"
end​

hello
# => "Hello, World"

​hello("Grant")
# => "Hello, Grant"​

3.times { hello("Grant") }
# => "Hello, Grant"
# => "Hello, Grant"
# => "Hello, Grant"

​def add(a, b)  
  return a + b
end​

add 4, 11
# => 15

​new_total = add 4, 11
new_total
# => 15
```

## Ruby - Collections <a id="ruby-collections"></a>

### Arrays <a id="arrays"></a>

#### _Creating an array_ <a id="creating-an-array"></a>

```ruby
# LITERAL CONSTRUCTOR
​
bros = []
bros = [ 'groucho', 'harpo', 'chico' ]
​
# CLASS KEYWORD
​
bros = Array.new # => []
bros = Array.new( 3 ) # => [ nil, nil, nil ]
bros = Array.new( 3, true ) # => [ true, true, true ]
# The parentheses are optional
​
bros = Array.new(4) { Hash.new } # => [{}, {}, {}, {}]
bros = Array.new(2) { Array.new(2) } # => [ [nil, nil], [nil, nil] ]
# The curly brackets are optional
​
# A FEW SHORTCUTS FOR CREATING BASIC ARRAYS
​
bros = 'groucho chico harpo'.split(' ') # => ['groucho', 'harpo', 'chico']
bros = %w(groucho harpo chico) # => ['groucho', 'harpo', 'chico']
# you can also use curly, square, or any character instead of the parentheses
# bros = %w !groucho, harpo, chico! => ['groucho', 'harpo', 'chico']
​
# CHARACTER MODIFIERS - http://en.wikibooks.org/wiki/Ruby_Programming/Syntax/Literals
​
%w{ Hello World }
%w[ Hello World ]
%w/ Hello World /
```

#### _Accessing elements of an array_ <a id="accessing-elements-of-an-array"></a>

```ruby
arr = [1, 2, 3, 4, 5, 6]
arr[2]      # => 3
arr[100]    # => nil
arr[-1]     # => 6
arr[-3]     # => 4
​
arr[2, 3]   # => [3, 4, 5]
# Adding an additional argument will return the more result depending on the number 
# given.
​
arr[1..4]   # => [2, 3, 4, 5]
arr[-1..-2] # => [5, 6]
​
# These work for reassignment as well!
​
arr[0] = 0
arr[0] = 1
​
arr.at(0)   # => 1
​
arr.first   # => 1
arr.last    # => 6
​
arr.take(3) # => [1, 2, 3] - Grabs the first three elements
arr.drop(3) # => [4, 5, 6] - Grabs the last three elements
​
arr.fetch(100) # => IndexError: index 100 outside of array bounds: -6...6
arr.fetch(100, "ERROR") # => "ERROR"
```

#### _Adding items to an array_ <a id="adding-items-to-an-array"></a>

```text
arr = [1, 2, 3, 4]
arr.push(5) # => [1, 2, 3, 4, 5]
arr << 6    # => [1, 2, 3, 4, 5, 6] Uses push behind the scenes
​
arr.unshift(9) # => [0, 1, 2, 3, 4, 5, 6] Adds an element to the start
​
arr.insert( 3, 'Serge' ) # => [ 0, 1, 2, 'Serge', 3, 4, 5, 6 ]
arr.insert( 4, 'didnt marry', 'Jane') 
# =>  [0, 1, 2, 'Serge', 'didnt marry', 'Jane', 3, 4, 5, 6]
```

#### _Removing items from an array_ <a id="removing-items-from-an-array"></a>

```ruby
# Pop removes the last element and returns it (it is destructive)
​
arr = [1, 2, 3, 4, 5, 6]
arr.pop     # => 6
arr         # => [1, 2, 3, 4, 5]
​
# To retrieve and at the same time remove the first item
​
arr.shift # => 1
​
# Delete at a particular index
​
arr.delete_at( 2 )
​
# To delete a particular element anywhere
​
arr = [1, 2, 2, 3]
arr.delete(2) # => [1, 3]
​
# Compact will remove nil values
​
arr = ['foo', 0, nil, 'bar', 7, 'baz', nil]
arr.compact  #=> ['foo', 0, 'bar', 7, 'baz']
​
# Remove duplicates
​
arr = [2, 5, 6, 556, 6, 6, 8, 9, 0, 123, 556]
arr.uniq    # => [2, 5, 6, 556, 8, 9, 0, 123]
```

#### _Iterating over arrays_ <a id="iterating-over-arrays"></a>

```ruby
arr = [1, 2, 3, 4, 5]
​
arr.each do |el|
  puts el
end
​
arr.each { |el| puts el }
​
arr.reverse_each do |el|
  puts el
end
​
arr.reverse_each { |el| puts el }
​
# The map method will create a new array based on the original one, but with the 
# values modified by the supplied block
​
arr = [1, 2, 3]
arr.map { |a| 2 * a }  # => Returns [ 2, 4, 6 ] but doesn't change the original
arr.map! { |a| 2 * a } # => Changes the original and returns it
​
# DON'T DO IT THESE WAYS!
​
arr = [1,2,3,4,5,6]
for x in 0..(arr.length-1)
  puts arr[x]
end
​
# or, with while:
x = 0
while x < arr.length
  puts arr[x]
  x += 1
end
​
for el in arr
  puts el
end
```

#### _Selecting items from an array_ <a id="selecting-items-from-an-array"></a>

Elements can be selected from an array according to criteria defined in a block. The selection can happen in a destructive or a non-destructive manner. While the destructive operations will modify the array they were called on, the non-destructive methods usually return a new array with the selected elements, but leave the original array unchanged.

```ruby
arr = [1, 2, 3, 4, 5, 6]
arr.select { |a| a > 3 }        # => [4, 5, 6]
arr.reject { |a| a < 4 }        # => [4, 5, 6]​

# You can use these two with the exclamation mark to make them destructive

​# The next two are destructive!

​arr.delete_if { |a| a < 4 }     # => [4, 5, 6]
arr.keep_if { |a| a < 4 }       # => [1, 2, 3]
```

#### _Ruby array comparison tricks_ <a id="ruby-array-comparison-tricks"></a>

```ruby
array1 = ["x", "y", "z"]
array2 = ["w", "x", "y"]

​array1 | array2
# Combine Arrays & Remove Duplicates(Union)
# => ["x", "y", "z", "w"]

​array1 & array2
# Get Common Elements between Two Arrays(Intersection)
# => ["x", "y"]​

array1 - array2
# Remove Any Elements from Array 1 that are contained in Array 2.(Difference)
# => ["z"]
```

Check out [this site](https://sites.google.com/site/dhtopics/Home/ruby-essentials/advanced-ruby-arrays)​

### _Ruby - Collections - Arrays - Exercises_ <a id="ruby-collections-arrays-exercises"></a>

* ​[Arrays Exercises​](https://gist.github.com/textchimp/042eabd499e6b73de064d3a557942ba7)

## Ruby Fundamentals - Part II <a id="ruby-fundamentals-part-ii"></a>

### Destructive methods vs non-destructive methods <a id="destructive-methods-vs-non-destructive-methods"></a>

There are destructive methods and non-destructive methods in Ruby. Destructive methods will affect the original, whereas non-destructive will leave it alone and just return an altered copy. Destructive methods normally end with an !.

### Predicate methods <a id="predicate-methods"></a>

More or less, predicate methods are those that return a boolean value. They always end with a ?.

### Blocks <a id="blocks"></a>

The content in iterators are called blocks, they are quite similar to anonymous functions in javascript.

```ruby
arr = [1, 2, 3]

​# The content between the do and the end is the block
arr.each do |el|    
  puts el
end

​# The content between the curly brackets is the block
arr.each { |el| puts el }
```

### Object IDs, strings vs. symbols, `false` interlude <a id="object-ids-strings-vs-symbols-false-interlude"></a>

In Ruby, every single thing is an object. Absolutely everything. Doesn't matter if it is a string, boolean or anything - they are all objects and all get assigned an object\_id. Every time a new one is created, even if it looks identical, a new object\_id \(a new place in memory\) will be created.

```ruby
"LUKE".object_id
# => 70131971988560

​{}.object_id
# => 70131953807740​

false.object_id
# => 0
```

Each time you reference a new string, hash or array, it declares a new object\_id - meaning that it takes up more memory in your Ruby program. If you imagine a database with thousands of entries, these small things add up to huge amounts of memory.

Symbols aren't like that, they are assigned a static place in memory \(meaning that they don't need to be redefined\). They behave in the exact same way as strings are easily translated back. Always use symbols for keys on objects.

```ruby
:name.object_id
# =>1147228
```

```ruby
# Conversions!​

:name.to_s
# => "name"​

"name".to_sym
# => :name
```

#### _False interlude_ <a id="false-interlude"></a>

The only things that are considered false in Ruby are the boolean `false`, and the `nil` value.

## Collections <a id="collections"></a>

### Hashes <a id="hashes"></a>

#### _Creation of a hash_ <a id="creation-of-a-hash"></a>

```ruby
# Literal Constructor
# "=>"" is called a hash rocket
​
hash = {}
serge = {
    :name => "Serge",
    :nationality => "French"
}
serge = {
    "name" => "Serge",
    "nationality" => "French"
}
serge = { # Keys stored as symbols!
    name: "Serge",
    nationality: "French"
}
# This will be automatically converted to 'hash rocket' styles
​
# Class Constructor
​
hash = Hash.new
​
# Normally a hash will return nil if the property is undefined
# We can pass in default values to this quite easily though
​
hash = Hash.new( "LUKE" )
hash["MILO"] #=> Will return "LUKE"
​
# If you create the hash using the literal though...
​
hash = {}
hash.default = false
hash["MILO"] #=> Will return false
```

#### _Accessing elements_ <a id="accessing-elements"></a>

```text
serge = { # Keys stored as symbols!
    name: "Serge",
    nationality: "French"
}
​
​
serge[:name]
​
serge = {
    "name" => "Serge",
    "nationality" => "French"
}
​
serge["name"]
```

#### _Adding items to a hash_ <a id="adding-items-to-a-hash"></a>

```ruby
# Notice no hash rocket!
​
serge[:counterpart] = "Jane (temporarily)"
​
# This is the same way as you access them!
​
p serge[:counterpart] # => "Jane (temporarily)"
```

#### _Removing items from a hash_ <a id="removing-items-from-a-hash"></a>

```ruby
serge.delete(:counterpart)
```

#### _Iterating over hashes_ <a id="iterating-over-hashes"></a>

```ruby
serge = { # Keys stored as symbols!
    name: "Serge",
    nationality: "French"
}
​
# Will run for keys and values
serge.each do |all|
    puts all
end
​
# Will run for each key and value pair
serge.each do |key, value|
    puts "Key: #{key} and Value: #{value}"
end
​
# Return the current key
serge.keys.each do |key|
    puts key
end
​
# Return the current value
serge.values.each do |value|
    puts value
end
​
# Thousands of other ways to do this though
```

### _Ruby - Collections - Exercises_ <a id="ruby-collections-exercises"></a>

* ​[Array and hash access​](https://gist.github.com/textchimp/480acdff23932574048601847ed3687e)

### _Ruby \(General\) - Recommended Readings_ <a id="ruby-general-recommended-readings"></a>

* ​[Why's \(Poignant\) Guide To Ruby](http://poignant.guide/)​
* ​[The Bastard's Book of Ruby](http://ruby.bastardsbook.com/)​

## Homework <a id="homework"></a>

* ​[MTA II - Ruby](https://gist.github.com/textchimp/86ad1ddd36cdc64a1f209d57488215cd)​
* [​Calculator​](https://gist.github.com/textchimp/c2736668175eba4cfe8802e2402cc74d)
* Also:
  * Watch [Pry - Introductory Screencast](http://pryrepl.org/)​
  * Browse [Ruby - Documentation](https://www.ruby-lang.org/en/documentation/)​

[  
](https://granthanrahan.gitbook.io/wdi27/daily-stuff/week-04)

