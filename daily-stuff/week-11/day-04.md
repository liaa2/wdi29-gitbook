# Day 04

What we covered today:

* Three.js
* Recursion



## Three.js <a id="three-js"></a>

## _Getting Started_ <a id="getting-started"></a>

Before you can use three.js, you need somewhere to display it. Save the following HTML to a file on your computer, along with a copy of three.js in the js/ directory, and open it in your browser.

```markup
<!DOCTYPE html>
<html>
    <head>
        <meta charset=utf-8>
        <title>My first three.js app</title>
        <style>
            body { margin: 0; }
            canvas { width: 100%; height: 100% }
        </style>
    </head>
    <body>
        <script src="js/three.js"></script>
        <script>
            // Our Javascript will go here.
        </script>
    </body>
</html>
```

### _Creating the scene_ <a id="creating-the-scene"></a>

To actually be able to display anything with three.js, we need three things: scene, camera and renderer, so that we can render the scene with camera.

```javascript
var scene = new THREE.Scene();
var camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
​
var renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );
```

We have now set up the scene, our camera and the renderer.

There are a few different cameras in three.js. For now, let's use a `PerspectiveCamera.`

The first attribute is the `field of view`. `FOV` is the extent of the scene that is seen on the display at any given moment. The value is in degrees.

The second one is the `aspect ratio`. You almost always want to use the width of the element divided by the height, or you'll get the same result as when you play old movies on a widescreen TV - the image looks squished.

The next two attributes are the `near and far clipping plane`. What that means, is that objects further away from the camera than the value of far or closer than near won't be rendered. You don't have to worry about this now, but you may want to use other values in your apps to get better performance.

Next up is the `renderer`. This is where the magic happens. In addition to the `WebGLRenderer` we use here, three.js comes with a few others, often used as fallbacks for users with older browsers or for those who don't have WebGL support for some reason.

In addition to creating the `renderer` instance, we also need to set the size at which we want it to render our app. It's a good idea to use the width and height of the area we want to fill with our app - in this case, the width and height of the browser window. For performance intensive apps, you can also give setSize smaller values, like `window.innerWidth/2` and `window.innerHeight/2`, which will make the app render at half size.

If you wish to keep the size of your app but render it at a lower resolution, you can do so by calling `setSize` with `false` as updateStyle \(the third argument\). For example, `setSize(window.innerWidth/2, window.innerHeight/2, false)` will render your app at half resolution, given that your `<canvas>` has 100% width and height.

Last but not least, we add the renderer element to our `HTML` document. This is a `<canvas>`element the renderer uses to display the scene to us.

```javascript
var geometry = new THREE.BoxGeometry( 1, 1, 1 );
var material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
var cube = new THREE.Mesh( geometry, material );
scene.add( cube );
​
camera.position.z = 5;
```

To create a cube, we need a `BoxGeometry`. This is an object that contains all the points \(vertices\) and fill \(faces\) of the cube.

In addition to the geometry, we need a material to color it. `Three.js` comes with several materials, but we'll stick to the `MeshBasicMaterial` for now. All materials take an object of properties which will be applied to them. To keep things very simple, we only supply a color attribute of `0x00ff00`, which is green. This works the same way that colors work in CSS or Photoshop \(hex colors\).

The third thing we need is a `Mesh`. A mesh is an object that takes a geometry, and applies a material to it, which we then can insert to our scene, and move freely around.

By default, when we call `scene.add()`, the thing we add will be added to the coordinates \(0,0,0\). This would cause both the camera and the cube to be inside each other. To avoid this, we simply move the camera out a bit.

### _Rendering the scene_ <a id="rendering-the-scene"></a>

If you copied the code from above into the HTML file we created earlier, you wouldn't be able to see anything. This is because we're not actually rendering anything yet. For that, we need what's called a render or animate loop.

```javascript
function animate() {
    requestAnimationFrame( animate );
    renderer.render( scene, camera );
}
animate();
```

This will create a loop that causes the `renderer` to draw the `scene` every time the screen is refreshed \(on a typical screen this means 60 times per second\). If you're new to writing games in the browser, you might say "why don't we just create a `setInterval`?" The thing is - we could, but `requestAnimationFrame` has a number of advantages. Perhaps the most important one is that it pauses when the user navigates to another browser tab, hence not wasting their precious processing power and battery life.

### _Animating the cube_ <a id="animating-the-cube"></a>

If you insert all the code above into the file you created before we began, you should see a green box. Let's make it all a little more interesting by rotating it.

Add the following right above the `renderer.render` call in your animate function:

```javascript
cube.rotation.x += 0.01;
cube.rotation.y += 0.01;
```

This will be run every frame \(normally 60 times per second\), and give the cube a nice rotation animation. Basically, anything you want to move or change while the app is running has to go through the animate loop. You can of course call other functions from there, so that you don't end up with a animate function that's hundreds of p.

## Recursion

Recursion in computer science is a method where the solution to a problem depends on solutions to smaller instances of the same problem \(as opposed to iteration\). Recursive algorithms have two cases: a recursive case and base case. Any function that calls itself is recursive.

Create a new folder and add a new ruby file into it.

```bash
mkdir recursion
cd recursion
touch countdown.rb
atom .
```

Iterative method:

```ruby
def countdown_i (n=10)
  while n >= 0
    puts n
    n -= 1
    sleep 1
  end
​
  puts "Blast off!"
​
end
​
require 'pry'
binding.pry
```

Call the method

```bash
ruby countdown.rb
countdown_i
```

Recursive method:

```ruby
def countdown_r (n=10)
  if n < 0 #Base case
    puts "Blast off"
  else
    puts n
    sleep 1
    countdown_r n-1 # Recursive case which moves us closer to the case
  end
end
​
require 'pry'
binding.pry
```

Call the method

```bash
ruby countdown.rb
countdown_r
```

Some things are better solved with recursion like factorials.

```bash
5! = 5 x 4 x 3 x 2 x 1
```

Create a new file.

```bash
touch factorial.rb
```

Iterative method:

```ruby
def factorial_i(n)
  result = 1
  while n > 1
    result = result * n # Mutation
    n -= 1 # Move closer to the base case
  end
  result
end
​
require 'pry'
binding.pry
```

Call the method

```ruby
ruby factorial.rb
factorial_i 5
```

Recursive method:

```ruby
def factorial_r(n)
  if n > 1 # Recursive case
    n * factorial_r(n -1)
  else
    1 # Base case
  end
end
​
require 'pry'
binding.pry
```

Call the method

```ruby
factorial.rb
factorial_r 5
```

Create another file. Fibonacci

```bash
touch fibonacci.rb
```

Iterative method:

```ruby
def fibonacci_i(n)
  a = 1
  b = 1
​
  while n > 1
    a, b = b, a + b  # Parallel assignment: a = b; b = a + b
    n -= 1
  end
  a # The final result will be in a
end
​
require 'pry'
binding.pry
```

Recursive method:

```ruby
# Very slow
def fibonacci_r(n)
​
  if n <= 2
    1 # Base case
  else
    fibonacci_r(n - 1) + fibonacci_r(n - 2)
  end
end
​
​
def factorial_r(n)
  if n > 1 # Recursive case
    n * factorial_r(n -1)
  else
    1 # Base case
  end
end

```

This example is extremely slow because we call the method twice with each iteration. This will exponential increase, doubling the If you call `fibonacci_r(100)` it looks for `fibonacci_r(98) + fibonacci_r(99)`. The problem is that it will then call `fibonacci_r()` twice for each of those `fibonacci_r(97) + fibonacci_r(98)`. As you can see you will be calling `fibonacci_r(98)` twice and create two copies of the branch even though you have already figured that out.  


### Further Reading <a id="further-reading"></a>

* ​[Beginning with 3D WebGL](https://codepen.io/rachsmith/post/beginning-with-3d-webgl-pt-1-the-scene)​
* ​[Animating Scenes with WebGL and Three.js](https://www.august.com.au/blog/animating-scenes-with-webgl-three-js/)​
* ​[Three.js Reddit](http://www.reddit.com/r/threejs/)​

