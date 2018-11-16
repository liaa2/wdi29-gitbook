# Day 04

What we covered today:

* 2D Graphics in the browser: P5.js
* Ruby on Rails - Testing continued



### Codealongs <a id="codealongs"></a>

* ​[2d graphics p5](https://github.com/textchimp/wdi-29/tree/master/week10/2d-graphics-p5)
* [Fruitstore TDD](https://github.com/textchimp/wdi-27/tree/master/week10/fruitstore-tdd)​

## P5

p5.js is a JavaScript library that starts with the original goal of [Processing](http://processing.org/), to make coding accessible for artists, designers, educators, and beginners, and reinterprets this for today's web.

Using the original metaphor of a software sketchbook, p5.js has a full set of drawing functionality.

Reference docs: [here](https://p5js.org/reference/)​

## Ruby on Rails - Testing - Rspec

#### Rspec and POST requests <a id="rspec-and-post-requests"></a>

So we are getting through all of this Rspec stuff but so far we have only done things like GET requests and checked existence of variables. Now we need to sort out validations such as POST requests and seeing how the page is actually rendered. It isn't overly difficult! This is a really basic version of it.

```ruby
describe 'POST to create' do
  describe "A fruit with valid information" do
    before do
      post :create, :params => { :fruit => { :name => "Strawberry" } }
    end
​
    it "should redirect to the show action" do
      # pending # Don't actually run this test!
      expect( response ).to redirect_to( assigns(:fruit) ) # Show page
    end
​
    it "should increase the number of fruits in the database"
      # pending
      expect( Fruit.count ).to eq( 1 )
    end
  end
​
  describe "A fruit with invalid information" do
    before do
      post :create, :params => { :fruit => { :name => "" } }
    end
​
    it "should give us a 200 success status" do
      # pending
      expect( response.status ).to eq( 200 )
    end
​
    it "should render the new template" do
      # pending
      expect( response ).to render_template( :new )
    end
​
    it "should not increase the number of fruits" do
      # pending
      expect( Fruit.count ).to eq( 0 )
    end
  end
end
```

The rails scaffold generates some pretty great tests, so make sure you check that out.

```bash
rails new scaffy -T --skip-git
cd scaffy
atom .
```

Add the 'rspec-rails' gem in the gem file.

```bash
gem 'rspec-rails'
```

```bash
bundle
rails generate rspec:install
rails generate scaffold Post title:string content:text author:string
```

Scaffolding has created a bunch of test automatically. You can check the below files to see how they have been set up.

```ruby
posts_routing_spec.rb
models/post_spec.rb
controllers/posts_controller_spec.rb
views/index_html_erb_spec.rb
```

Worth checking out [betterspecs](http://betterspecs.org/) as well. It's crowdsourced advice on how to write good tests.

### Homework <a id="homework"></a>

* Interview Questions II 
* more Learnyounode
* p5 experiments
* think about final projects
* identify and review/get help with your weak spots



