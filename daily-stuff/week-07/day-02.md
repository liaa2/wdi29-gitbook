# Day 02

What we covered today:

* JavaScript - AJAX with jQuery
* JavaScript - Same Origin Policy
* AJAX on Rails

### Warmup <a id="warmup"></a>

* ​[Text Soup2](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week07/day02_textsoup2)

### Codealongs <a id="codealongs"></a>

* [​AJAX jQuery](https://github.com/textchimp/wdi-29/tree/master/week7/ajax-jquery)
* ​[AJAX on Rails​](https://github.com/textchimp/wdi-29/tree/master/week7/ajax-on-rails)

## JavaScript - AJAX with jQuery <a id="javascript-ajax-with-jquery"></a>

jQuery gives us a bunch of methods that make AJAX a lot easier.

### How to do it <a id="how-to-do-it"></a>

There are so many ways of using AJAX with jQuery. The most flexible is using the `$.ajax` method, which has been around since jQuery 1.0. All of the other AJAX methods that you can use with jQuery use this behind the scenes.

```javascript
// Basic syntax:
$.ajax( url, { OPTIONS } );
// Example:
$.ajax( "/stats", { method: "GET" } );
​
// Preferred syntax:
$.ajax({ OPTIONS });
// Preferred syntax example:
$.ajax({
  url: '/post',
  type: 'GET',
  // etc
})
```

Here is a more complex example using the preferred syntax.

```javascript
// Using the core $.ajax() method
$.ajax({
​
    // The URL for the request
    url: "/post",
​
    // The data to send (will be converted to a query string)
    data: {
        id: 123
    },
​
    // The type of request
    type: "GET",
​
    // The type of data we expect back
    dataType : "json",
​
    // Code to run if the request succeeds.
    // The responseText is passed to the 'success' function as the 'data' argument
    success: function( data ) {
        $( "<h1>" ).text( data.title ).appendTo( "body" );
        $( "<div class=\"content\">").html( data.html ).appendTo( "body" );
    },
​
    // Code to run if the request fails.
    // The request, the status code of the request and the error thrown are passed to the 'error' function as arguments
    error: function( xhr, status, errorThrown ) {
        alert( "Sorry, there was a problem!" );
        console.log( "Error: " + errorThrown );
        console.log( "Status: " + status );
        console.dir( xhr );
    },
​
    // Code to run when the request is completed, regardless of success or failure
    complete: function( xhr, status ) {
        console.log( "The request is complete." );
    }
​
});
```

We could also use promises for this, instead of encapsulating the handlers \(success, error etc.\). We can chain jQuery AJAX methods together, and jQuery 'promises' that these will get run.

```javascript
$.ajax({...}).always(function () {
    // This will always run
}).done( function (data) {
    // This will run on success.
}).fail( function (data) {
    // This will run if there is an error
});
```

### jQuery AJAX convenience methods <a id="jquery-ajax-convenience-methods"></a>

jQuery also offers a number of 'convenience methods' that use `$.ajax` behind the scenes. These are shorthand for more complicated `$.ajax` functions, meaning they're simpler to write, but less customizable.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Convenience Method</th>
      <th style="text-align:left">Long form $.ajax function</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">​<a href="http://api.jquery.com/jQuery.get/">$.get</a>​</td>
      <td style="text-align:left">
        <p><code>$.ajax({</code> 
        </p>
        <p><code>  dataType: dataType,</code> 
        </p>
        <p><code>  url: url,</code> 
        </p>
        <p><code>  data: data,</code> 
        </p>
        <p><code>  success: success</code> 
        </p>
        <p><code>});</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://api.jquery.com/jQuery.getJSON/">$.getJSON</a>​</td>
      <td
      style="text-align:left">
        <p><code>$.ajax({</code> 
        </p>
        <p><code>  dataType: &quot;json&quot;,</code> 
        </p>
        <p><code>  url: url,</code> 
        </p>
        <p><code>  data: data,</code> 
        </p>
        <p><code>  success: success</code> 
        </p>
        <p><code>});</code>
        </p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://api.jquery.com/jQuery.getScript/">$.getScript</a>​</td>
      <td
      style="text-align:left">
        <p><code>$.ajax({</code> 
        </p>
        <p><code>  dataType: &quot;script&quot;,</code> 
        </p>
        <p><code>  url: url,</code> 
        </p>
        <p><code>  success: success</code> 
        </p>
        <p><code>});</code>
        </p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://api.jquery.com/jQuery.post/">$.post</a>​</td>
      <td style="text-align:left">
        <p><code>$.ajax({</code> 
        </p>
        <p><code>  type: &quot;POST&quot;</code> 
        </p>
        <p><code>  dataType: dataType,</code> 
        </p>
        <p><code>  url: url,</code> 
        </p>
        <p><code>  data: data,</code> 
        </p>
        <p><code>  success: success</code> 
        </p>
        <p><code>});</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>### jQuery `.load` <a id="jquery-load"></a>

### _JavaScript - AJAX with jQuery - Further Reading_ <a id="javascript-ajax-with-jquery-further-reading"></a>

* ​[jQuery Fundamentals - AJAX & Deferreds](http://jqfundamentals.com/chapter/ajax-deferreds)​
* ​[Learn jQuery - jQuery AJAX methods](https://learn.jquery.com/ajax/jquery-ajax-methods/)​
* ​[jQuery API Documentation - $.ajax](http://api.jquery.com/jquery.ajax/)​

## JavaScript - Same Origin Policy <a id="javascript-same-origin-policy"></a>

The 'Same Origin Policy' is a browser security mechanism that restricts how a document or script loaded from one 'origin' can interact with a resource from another 'origin'.

An 'origin', in this context, is the combination of the protocol, port and host - you can generally just think of this as the 'domain'. The Same Origin Policy states that JavaScript that originated from one domain cannot request a resource from another domain. A request that breaches this protocol will generally respond with a 'No Cross-Origin Resource Sharing' error \(a **CORS** error\) in the developer tools console.

CORS errors are not easy to deal with.

### Cross Origin Resource Sharing <a id="cross-origin-resource-sharing"></a>

A resource's Cross Origin Sharing policy can be checked by:

1. Sending an AJAX request to the URL \(eg `$.ajax('http://www.smh.com.au')`\):
   * If Cross Origin Resource Sharing is allowed, this will return an object with no errors;
   * If Cross Origin Resource Sharing is **not** allowed, this will return a CORS error along the following lines:

     ```bash
     XMLHttpRequest cannot load http://www.some-website.com/. 
     No 'Access-Control-Allow-Origin' header is present on the requested resource. 
     Origin '[your_URL]' is therefore not allowed access.
     ```
2. Checking the Cross Origin Resource Sharing policy in the HTML's response headers - open up your browser's developer tools, click 'Network', select the document and look under the 'Response Headers':
   * If Cross Origin Resource Sharing is allowed, you will see something like: `Access-Control-Allow-Origin: *`

Websites can allow different levels of Cross Origin access - see the MDN Article on HTTP Access Control \(CORS\), below.

There are a few ways to deal with CORS errors, but they generally rely on the host of the resource you're trying to access accommodating your needs. The origin needs to:

* Allow CORS; or
* Support JSONP\*; or
* Host your code.

\* JSONP \('JavaScript Browser Notation With Padding'\) is a super basic form of authentication. JSONP sends the server some information about the client \(eg, the client's IP address\) in the request headers, and allows the server to track use of their API, and prevent abuse of their API \(eg, by denying repeated requests from the same IP address\).

#### _Dealing with CORS in development_ <a id="dealing-with-cors-in-development"></a>

Cross-Origin Resource Sharing is \(for our purposes\) only supported by http and https. Often when we're developing front-end components, we won't have a server running, meaning the protocol being used will be `file://` \(not `http://` or `https://`\), which will result in a CORS error \(visible in the console\). The easiest way to get around this is to use Python's SimpleHTTPServer module, instead of just opening the html directly in the browser using `file://` \(eg, via Atom's Open In Browser package\).

The following terminal command will create a web server using the contents of the current working directory:

```bash
python -m SimpleHTTPServer
# => Serving HTTP on 0.0.0.0 port 8000 ...
```

Then navigate to **localhost:8000** in your browser.

## JavaScript - AJAX on Rails <a id="javascript-ajax-on-rails"></a>

Quick recap:

* Our rails server responds to HTTP requests to particular URLs.
* The router maps URL paths to controller actions, routing HTTP requests to the appropriate action based on the URL requested by the client.
* The controller action is executed, and - where necessary - a response is rendered to the client.

Up to this point, the controller has been rendering HTML in response to all HTTP requests, but a concept at the core of single-page applications is to respond to HTTP requests with JSON objects \(rather than HTML\), and update only those parts of the page that require updating, rather than re-rendering the entire page.

Rails works really well with AJAX and JSON objects. We can:

1. Render JSON in response to `GET` requests set via AJAX, by processing the request in the controller alone.
2. Retrieve data from the database and render JSON in response to `GET` requests sent via AJAX.
3. Destroy records in the database in response to `DELETE` requests sent via AJAX.
4. Update records in the database in response to `POST`/`PUT` sent via AJAX.

### Render JSON in response to `GET` requests set via AJAX, by processing the request in the controller alone <a id="render-json-in-response-to-get-requests-set-via-ajax-by-processing-the-request-in-the-controller-alone"></a>

This example illustrates how we can process a request made to a particular URL and send a response from the controller, without fetching any data from the database.

Our application will generate random cat names, because of course it will.

#### _Create a new Rails app_ <a id="create-a-new-rails-app"></a>

In terminal:

```bash
  rails new ajax_rails --skip-git --skip-turbolinks -d postgresql
  rails generate controller Pages index
```

#### _Set up our routes_ <a id="set-up-our-routes"></a>

In **config/routes.rb:**

```ruby
# This will show app's single 
page:root 'pages#index'
# Our AJAX requests will be sent to this path:
get "/generator" => "pages#generator"
```

#### _Set up our app's single HTML view_ <a id="set-up-our-apps-single-html-view"></a>

In **app/views/pages/index.html/erb**:

```markup
<button id="cat-name">Cat Name Generator</button>
​
<p>Introducing
  <span id="title"></span>
  <span id="name"></span>
  <span id="surname"></span>
</p>
```

#### _Set up our controller actions_ <a id="set-up-our-controller-actions"></a>

Our application is going to have two actions: an `index` action, and a `generator` action. Only the `index` action will render HTML; the `generator` action will render JSON.

By default, the controller will look for an HTML template app/views/pages\|layouts/generator.html in response to requests to the `/generator` path. But we want the action to send JSON to the browser. Here's the line we'll add to the end of our `generator` action in **app/controllers/pages\_controller.rb** to get this to work:

```ruby
def generator  
  render :json => @generated_name
end
```

Two things are happening here: firstly, our action will render `@generated_name` as JSON instead of HTML. Secondly, the `:json` method will call `.to_json` on the `@generated_name` object, converting it to a JSON object that we can access and manipulate in using JavaScript before it is rendered by the browser.

Now we're going to add the logic the server needs to process the request to our controller. We'll create a hash of cat name options, randomly select values from that hash and store them in an instance variable called `@generated_name` which we'll send to the browser as a JSON object.

```ruby
class PagesController < ApplicationController
  def index
  end
​
  def generator
    options = {
      male: {
        titles: ["Mr ", "Lord ", "Count ", "Sir ", "His Lordship, "],
        names: ["Lewis ", "Felix ", "Baxter "]
      },
      female: {
        titles: ["Ms ", "Lady ", "Countess ", "Baroness ", "Her Ladyship, "],
        names: ["Kristy ", "Liesl ", "Pia "]
      },
      surnames: ["Bergstrom", "Eckersley", "Weinberg"]
    }
​
    random = ["male", "female"].sample.to_sym
​
    @generated_name = {
      :title => options[random][:titles].sample,
      :name => options[random][:names].sample,
      :surname => options[:surnames].sample
    }
​
    render :json=> @generated_name
  end
end
```

If we wanted our application to be able to render both HTML and JSON in response to requests to the `/generator` URL, we could use Rails' `respond_to` method to respond to different request formats. Why would we do this? Just say we wanted to be able to render HTML in our own application's UI, but also wanted to open up our application as an API to other applications. We'd first have to create a new **app/views/pages/generator.html.erb** view to render our HTML. Then, our `render` line could be changed as follows to allow this:

```ruby
respond_to do |format|
  # This will render generator.html in response to requests for HTML
  format.html 
  # This will render JSON to AJAX requests
  format.json { render json: @generated_name } 
end
```

#### _Set up our AJAX request and response handler_ <a id="set-up-our-ajax-request-and-response-handler"></a>

Create a new file **app/assets/javascripts/generator.js**.

We need to:

1. Add an event listener to the button.
2. Create a function that will send a `GET` request via AJAX to the path `/generator`.
3. Include a `.done` function that will handle the JSON response returned by the server and update the page.

```javascript
$(document).ready(function() {
​
  var randomName = function() {
    $.ajax({
      url: '/generator',
      type: "GET",
      dataType: "JSON"
    }).done(function(data) {
       $("#title").text(data.title);
       $("#name").text(data.name);
       $("#surname").text(data.surname);
    });
  };
​
  $("button").on("click", randomName);
​
});
```

Open your server \(`rails s`\) and you should be able to generate a cat name!

### Retrieve data from the database and render JSON in response to `GET` requests sent via AJAX <a id="retrieve-data-from-the-database-and-render-json-in-response-to-get-requests-sent-via-ajax"></a>

This example illustrates how we can retrieve data from our database and send it back to the browser in response to an AJAX request made to a particular URL, which is - arguably - more useful than just getting our controller to generate a random cat name.

In this example we won't be just sending back a record \(or series or records\), we'll be sending back:

* A record;
* That record's _associated_ records;
* What a particular method in that record's model returns.

Let's use the app created above as a starting point.

#### _Scaffold some models_ <a id="scaffold-some-models"></a>

In terminal:

```bash
  rails generate scaffold Habitat name:string
  rails generate scaffold Species name:string status:string habitat:references
  rails generate scaffold Animal name:string color:string species:references
```

#### _Update our models' associations_ <a id="update-our-models-associations"></a>

The scaffold will have set up the `belongs_to` associations for you \(both the migrations with the necessary foreign keys and the associations on our models\), but you'll need to add the `has_many` associations to your models.

We're also going to add another method to the Animal class that we can call on an animal object to get information about the animal's climate. We'll see below how we can include this method in our JSON response.

Update your models so they look like this:

```ruby
# in app/models/animal.rb
class Animal < ActiveRecord::Base
  belongs_to :species
​
  def climate
    if self.species.habitat.name == "Alpine"
      "Cold"
    else
      "Maybe not too cold"
    end
  end
end
​
end
​
# in app/models/species.rb
class Species < ActiveRecord::Base
  has_many :animals
  belongs_to :habitat
end
​
# in app/models/habitat.rb
class Habitat < ActiveRecord::Base
  has_many :species
end
```

Now we'll have the following models and associations:

* Animal `belongs_to :species`
* Species `belongs_to :habitat`, `has_many :animals`
* Habitat `has_many :species`

#### _Set up our database_ <a id="set-up-our-database"></a>

In **db/seeds.rb**:

```ruby
h1 = Habitat.create({:name => "Woodland"})
h2 = Habitat.create({:name => "Alpine"})
​
s1 = Species.create({:name => "Meles meles", :status => "Not endangered"})
s2 = Species.create({:name => "Martes americana", :status => "Endangered"})
s3 = Species.create({:name => "Mustela putorius", :status => "Endangered"})
​
a1 = Animal.create({:name => "Badger", :color => "Black and white"})
a2 = Animal.create({:name => "Pine marten", :color => "Brown and white"})
a3 = Animal.create({:name => "Polecat", :color => "White"})
​
s1.animals << a1
s2.animals << a2
s3.animals << a3
​
h1.species << s1
h2.species << s2 << s3
```

Then, in terminal:

```ruby
rails db:create
rails db:migrate
rails db:seed
```

#### _Set up a route_ <a id="set-up-a-route"></a>

We're going to put an additional route to handle AJAX requests to get more details about our animals. Any `GET` requests to the URL `/details/{something}` will be routed to a `details` action in the `animals_controller`.

Add the following to your **config/routes.rb** file

```ruby
  get 'details/:id' => "animals#details", :as => 'details'
```

#### _Configure the controller_ <a id="configure-the-controller"></a>

We need to create a `details` action in **app/controllers/animals\_controller.rb**. In there, we'll be retrieving the records we want from the database and sending certain details of those records \(and those records' associated records\) back to the browser as JSON objects.

```ruby
# ...
def details
​
  # Get an animal record from the database using the ID in params.
  @animal = Animal.find(params[:id])
​
  # If we just want to return details of the record represented by the @animal object, we could now simply do:
​
  # render :json => @animal
​
  # But if we want to get details of OTHER records associated with the @animal object, we need to call .to_json on the @animal object, and specify what associated records we want to include, and what attributes of those associated records we want to include/exclude.
  @response = @animal.to_json(
  :methods => :climate,
  :include => {
    :species => {
      :except =>
        [:created_at, :updated_at],
      :include => {
        :habitat => {
          :only => :name
        }
      }
    }
  })
​
  # Then we render the response as :json. This lets Rails know to render a JSON object back to the browser, rather than an HTML view.
​
  render :json => @response
  # ...
end
```

If you open up the URL **localhost:3000/details/1** in the browser, you should see a representation of a JSON object relating to the first record in our database's animals table.

#### _Set up a view_ <a id="set-up-a-view"></a>

First, delete all the content in the template **app/assets/views/animals/index.html.erb**, and replace it with the following:

```markup
<% @animals.each do |animal| %>
  <div id="#{animal.id}">
  <%= link_to(animal.name, details_path(animal.id), remote: true, :class => "get-animal") %>
  </div>
<% end %>
<div class="response-text"></div>
```

This is going to create a link to the `details_path`, which will be routed to the `details` action in our `animals controller`. Notice the `remote: true` - this will add the HTML attribute `data-remote=true` to the `a` element generated by the `link_to` helper, and tells the browser to send the request to the server using AJAX. We're also giving the `div` the class of the animal's ID to make it easier to remove the element from the DOM \(in response to a successful delete request, which we'll do a bit later\).

We've also created a `div` element \(with the class `response-text`\) where we'll be putting parts of the response text returned by the server.

#### _Set up the AJAX response handler_ <a id="set-up-the-ajax-response-handler"></a>

Now we'll use JavaScript to handle the response from the server and render it in the browser.

I'm going to rename the **app/assets/javascripts/animals.coffee** generated by the scaffolding to **app/assets/javascripts/animals.js** and put all my JavaScript in there.

To start with, I'd put a `debugger` in the jQuery AJAX response handler, so I can figure out how to access the data we need in the object that the request returns, but we'll skip over that step below.

We can pass up to four arguments into the AJAX response handlers - the `event` \(particularly useful if we want to manipulate the element that was clicked on\), the `data` \(the JSON object returned by the controller\), the `status` \(eg 'success', 'error'\) and the full `xhr` response. We'll only be using the `data` here.

```javascript
$(document).ready(function() {
  $(".get-animal").on("ajax:success", function(event, data, status, xhr) {
    // debugger
    $animal = $("<p>").text("Animal: " + data.name);
    $species = $("<p>").text("Species: " + data.species.name);
    $status = $("<p>").text("Habitat: " + data.species.habitat.name);
    $(".response-text").empty().append($animal).append($species).append($status);
  }).on("ajax:error", function() {
    $error = $("<p>").text("An error occurred. That's all we know.");
    $(".response-text").empty().append($error);
  });
});
```

Browse to **localhost:3000/animals** and you should be able to click on an animal's name and see the page update with data from the database without the browser reloading the whole page.

### Destroy records in the database in response to `DELETE` requests sent via AJAX <a id="destroy-records-in-the-database-in-response-to-delete-requests-sent-via-ajax"></a>

This is pretty straightforward. We need to:

1. Add another link to our view
2. Slightly modify how the `destroy` action in the controller will repond to a `DELETE` request
3. Add another AJAX handler to our JavaScript.

#### _Update the view_ <a id="update-the-view"></a>

We need to add another link to our view, and set the HTTP method to `DELETE`.

In **app/assets/views/animals/index.html**, add the lines between the comments:

```markup
<% @animals.each do |animal| %>
  <div id=<%= animal.id %>>
    <%= link_to(animal.name, details_path(animal.id), remote: true, :class => "get-animal") %>
    <!-- AJAX DELETE -->
    <%= link_to("Delete Animal", animal_path(animal.id), remote: true, method: :delete, :class => "delete-animal", "data-type" => :json) %>
    <!-- end AJAX DELETE -->
  </div>
<% end %>
<div class="response-text"></div>
```

#### _Reconfigure the controller_ <a id="reconfigure-the-controller"></a>

In **app/controllers/animals\_controller.rb**, change the `destroy` action send back the deleted animal record as JSON \(so we can delete the DOM elements relating to that record\).

```ruby
class AnimalsController < ApplicationController
  # ...
  def destroy
    @animal.destroy
    respond_to do |format|
      format.html { redirect_to animals_url, notice: 'Animal was successfully destroyed.' }
      format.json { render :json => @animal }
    end
  end
  # ...
end
```

#### _Set up the AJAX response handler_ <a id="set-up-the-ajax-response-handler-1"></a>

In **app/assets/javascript/animals.js**, add the following:

```javascript
$(".delete-animal").on("ajax:success", function(event, data, status, xhr) {
  $("#" + data.id).remove();
  $(".response-text").empty().append("Animal deleted");
}).on("ajax:error", function() {
  $error = $("<p>").text("An error occurred. That's all we know.");
  $(".response-text").empty().append($error);
});
```

This will find the element with the ID returned in the ID property of the `data` response and remove it from the DOM, as well as displaying a notice to the user that an Animal was successfully deleted.

### Update records in the database in response to `POST`/`PUT` sent via AJAX <a id="update-records-in-the-database-in-response-to-post-put-sent-via-ajax"></a>

Let's build on the work we've done so far by allowing users to update records without the page being reloaded \(ie, without a new HTML page being sent to the browser\). This follows a similar approach to the `DELETE` request above.

Let's start by changing the **app/views/animals/index.html.erb** to include forms that will allow users to change the `color` attribute of animal records from that view.

Submitting one of these forms will send a `PUT/PATCH` request to the controller to update a particular animal record \(since it already exists\).

```markup
<% @animals.each do |animal| %>
  <div id= <%= animal.id %> >
    <%= link_to(animal.name, details_path(animal.id), remote: true, :class => "get-animal") %>
    <%= link_to("Delete Animal", animal_path(animal.id), remote: true, method: :delete, :class => "delete-animal", "data-type" => :json) %>
    <!-- AJAX PUT/PATCH  -->
    <%= form_for(animal, remote: true, format: :json) do |f| %>
      <%= f.label :color %>
      <%= f.text_field :color, :value => animal.color %>
      <%= f.submit "update" %>
    <% end %>
    <!-- end AJAX PUT/PATCH -->
  </div>
<% end %>
<div class="response-text"></div>
```

#### _Reconfigure the controller_ <a id="reconfigure-the-controller-1"></a>

For this, we're going to change the `update` method so that it just returns a very basic success/failure response \(since we don't really need to retrieve anything from the database\).

Our AJAX response handler is expecting JSON to be returned by the controller, so we do need to send back a JSON object of some kind, but we're just going to send back an object with HTTP status codes only \(`:ok` representing a successful `200` HTTP status, `:unprocessable_entity` representing a failed `422` HTTP status\).

This isn't really necessary, but it's worth checking out the different kinds of responses your controllers can send.

```ruby
def update
  respond_to do |format|
    if @animal.update(animal_params)
      format.html { redirect_to @animal, notice: 'Animal was successfully updated.' }
      format.json { render :json => {status: :ok} }
    else
      format.html { render :edit }
      format.json { render :json => {status: :unprocessable_entity} }
    end
  end
end
```

#### _Set up the AJAX response handler_ <a id="set-up-the-ajax-response-handler-2"></a>

This is going to look pretty similar to our AJAX handler for the `DELETE` request. All this will do is render some text on the page indicating whether the update was successful or not.

Rails is going to generate our forms with the class of "edit\_animal". We're going to add the AJAX event listener to the form itself - this says "listen for any forms with this class being submitted", which is pretty handy \(our listener is bound to the form, and is listening for the submit event, rather than being bound to an click even on an arbitrary button\).

```javascript
$(".edit_animal").on("ajax:success", function(event, data, status, xhr) {
  $(".response-text").empty().append("Animal updated");
}).on("ajax:error", function() {
  $error = $("<p>").text("An error occurred. That's all we know.");
  $(".response-text").empty().append($error);
});
```

### _JavaScript - Same Origin Policy - Further Reading_ <a id="javascript-same-origin-policy-further-reading"></a>

* ​[MDN - Same Origin Policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)​
* ​[MDN - HTTP Access Control \(CORS\)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)​

### _JavaScript - APIs - Useful Links_ <a id="javascript-apis-useful-links"></a>

* ​[GitHub - Todd Motto - Public APIs](https://github.com/toddmotto/public-apis)​

### _AJAX on Rails - Further Reading_ <a id="ajax-on-rails-further-reading"></a>

* ​[Rails Guides - Working with JavaScript in Rails](http://guides.rubyonrails.org//v4.2/working_with_javascript_in_rails.html)​
* ​[Rails Guides - Layouts and Rendering in Rails](http://guides.rubyonrails.org/v4.2/layouts_and_rendering.html)​
* ​[API Dock - ActiveModel JSON Serializers](http://api.rubyonrails.org/classes/ActiveModel/Serializers/JSON.html)​

### Homework <a id="homework"></a>

Build a cool single page thing using an API. Some resources:

* ​[Nasa API](https://api.nasa.gov/)​
* ​[International Space Station API](http://open-notify.org/Open-Notify-API/ISS-Location-Now/)​
* ​[Wikipedia API](https://www.mediawiki.org/wiki/API:Main_page)​
* ​[Wolfram alpha API](http://products.wolframalpha.com/api/)​
* ​[Air Quality](https://docs.openaq.org/)​
* ​[Beer Brewery](https://docs.openaq.org/)​
* ​[Movie DB](https://developers.themoviedb.org/3)​
* ​[Star Wars](https://swapi.co/)​
* ​[Pokemon API](http://pokeapi.co/)​
* ​[Donald Trump Quotes](https://docs.tronalddump.io/)​
* ​[Marvel API](https://developer.marvel.com/)​
* ​[Aus census API](https://www.data.gov.au/)​
* ​[Other open APIs](https://github.com/toddmotto/public-apis)​
* ​[Wiki list of open APIs](https://en.wikipedia.org/wiki/List_of_open_APIs)​
* ​[The open web list of APIs](https://www.programmableweb.com/category/all/apis)​

Further reading:

* ​[AJAX resources](https://gist.github.com/wofockham/3d4faf65dc9a5674ce11)​

