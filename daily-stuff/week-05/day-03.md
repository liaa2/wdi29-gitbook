# Day 03

What we covered today:

* Ruby on Rails - Associations
* **Guest speaker**: Daisy Smith - [Creative Coding](https://docs.google.com/presentation/d/1qSPH6f2j1vX7K5HUbQ1id88m5ZQ94PRBFudGXnHrlws/edit#slide=id.g38042e32c5_0_37)

### Warmup {#warmup}

* [​Atbash Cipher - Ruby​](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week05/day03_atbash_cipher)

### Classwork {#classwork}

* ​[MoMA​](https://github.com/textchimp/wdi-29/tree/master/week5/moma-app)

## Ruby on Rails - Basic Project Setup \(with 2 models\) {#ruby-on-rails-basic-project-setup-with-database}

Treat this as a really rough guide, and definitely don't always follow it - you'll figure out your approach soon. This is a basic approach you might follow when setting up a new Rails project:

| Step | What | Where | How |
| :--- | :--- | :--- | :--- |
| 1 | Planning | - | Pen & paper |
| 2 | Create a new Rails app | Terminal | `rails new kitten_party --skip-git --skip-turbolinks` |
| 3 | Move into the new app's dir | Terminal | `cd kitten_party` |
| 4 | Add development Gems | /Gemfile | `gem "pry-rails"` |
| 5 | Bundle Gems | Terminal | `bundle` |
| 6 | Create database | Terminal | `rails db:create` |
| 7 | Generate first model | Terminal | `rails generate model Kitten name:string age:integer` |
| 8 | Edit migration as required | /db/migrate/\[your\_migration\].rb | Add timestamps, more columns, etc if required. |
| 9\* | Generate first controller | Terminal | `We will do it manually for now (go to the controller folder and create a controller file called "kittens_controller.rb")` |
| 10 | Add methods to the controller | /app/controllers/kittens\_controller.rb | Add methods for each action |
| 11 | Add views for your actions | /app/views/kittens/ | Add an \[action\].html.erb file for each action that has an associated view |
| 12 | Configure routes | /config/routes.rb | `root :to => "kittens#index"` `resources :kittens` |
| 13 | Repeat for other models | - | Repeat steps 7-12 for each model |

\* You can specify the actions for which you would like Rails to create views and methods when generating the controller by adding them to the end of the command - eg `rails generate controller Kittens index show edit new`. This will create those views, and the placeholder methods in your controller, but it also generates a bunch of routes that you will probably want to delete.

## Ruby on Rails - Associations I {#ruby-on-rails-associations}

Associations allow you to create relationships between any two models \(that inherit from ActiveRecord::Base\). By declaratively telling Rails that two models have a certain association with each other, we can greatly streamline our code.

Rails supports six types of associations, the two simplest associations are `belongs_to` and `has_many`.

### `belongs_to` {#belongs_to}

A belongs\_to association sets up a one-to-one connection with another model, such that each instance of the declaring model "belongs to" one instance of the other model. For example, if your application includes customers and orders, and each order can be assigned to exactly one customer, you'd declare the order model this way:

```ruby
  class Order < ActiveRecord::Base
    belongs_to :customer, optional :true
  end
```

A few things to note about `belongs_to` associations:

* The singularized form of the 'other' model \(`customer`\) _must_ be used for the association to work.
* The `order` table must also include the `customer_id` for the customer records to which it belongs.
* A `belongs_to` association often has a reciprocal `has_one` or `has_many` association on the other model.

### `has_many` {#has_many}

A has\_many association indicates a one-to-many connection with another model. You'll often find this association on the "other side" of a belongs\_to association. This association indicates that each instance of the model has zero or more instances of another model. For example, in an application containing customers and orders, the customer model could be declared like this:

```ruby
class Customer < ActiveRecord::Base
  has_many :orders
end
```

A few things to note about `has_many` associations:

* The pluralized form of the 'other' model \(`orders`\) _must_ be used for the association to work.
* A `has_many` association often has a reciprocal `belongs_to` association on the other model.
* The model with the `has_many` association doesn't store the 'foreign key' of the related model. That goes on the model with the `belongs_to` association.

### _Ruby on Rails - Associations_ {#ruby-on-rails-associations-1}

* ​[Rails Guides - Association Basics](http://guides.rubyonrails.org/v4.2/association_basics.html)​

### Homework {#homework}

* DIY Rails App - Build your own Rails app from scratch, including CRUD \(with 2 models, and working associations\)
* Read:
  * ​[Rails Guides - Active Record Migrations](http://guides.rubyonrails.org/v4.2/active_record_migrations.html)​
  * ​[Rails Guides - Active Record Associations](http://guides.rubyonrails.org/v4.2/association_basics.html)​

