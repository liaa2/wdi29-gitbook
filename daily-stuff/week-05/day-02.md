# Day 02

What we covered today:

* Ruby on Rails - Basic Project Setup \(with database\)

### Warmup {#warmup}

* Robot factory - Ruby​

### Classwork {#classwork}

* ​Movie-search
* ​[p](https://github.com/textchimp/wdi-29/tree/master/week5/rails-stocks)lanets-db

## Ruby on Rails - Basic Project Setup \(with database\) {#ruby-on-rails-basic-project-setup-with-database}

Treat this as a really rough guide, and definitely don't always follow it - you'll figure out your approach soon. This is a basic approach you might follow when setting up a new Rails project:

| Step | What | Where | How |
| :--- | :--- | :--- | :--- |
| 1 | Planning | - | Pen & paper |
| 2 | Create a new Rails app | Terminal | `rails new kitten_party` |
| 3 | Move into the new app's dir | Terminal | `cd kitten_party` |
| 4 | Add development Gems | /Gemfile | `gem "remove_turbolinks"` `group :development do` `gem "pry-rails"` `gem "pry-stack_explorer"` `gem "annotate"` `gem "quiet_assets"` `gem "better_errors"` `gem "binding_of_caller"` `gem "meta_request"` `end` |
| 5 | Bundle Gems | Terminal | `bundle` |
| 6 | Create database | Terminal | `rake db:create` |
| 7 | Generate first model | Terminal | `rails generate model Kitten name:string age:integer` |
| 8 | Edit migration as required | /db/migrate/\[your\_migration\].rb | Add timestamps, more columns, etc if required. |
| 9\* | Generate first controller | Terminal | `rails generate controller Kittens` |
| 10 | Add methods to the controller | /app/controllers/kittens\_controller.rb | Add methods for each action |
| 11 | Add views for your actions | /app/views/kittens/ | Add an \[action\].html.erb file for each action that has an associated view |
| 12 | Configure routes | /config/routes.rb | `root :to => "kittens#index"` `resources :kittens` |
| 13 | Repeat for other models | - | Repeat steps 7-12 for each model |

\* You can specify the actions for which you would like Rails to create views and methods when generating the controller by adding them to the end of the command - eg `rails generate controller Kittens index show edit new`. This will create those views, and the placeholder methods in your controller, but it also generates a bunch of routes that you will probably want to delete.

## Ruby on Rails - Migrations {#ruby-on-rails-migrations}

Migrations are a way to modify your database schema using Ruby code. Using migrations, we can:

* Avoid writing SQL by hand;
* Change our database schema progressively over time;
* Roll back to earlier versions of our database schema;
* Rebuild our database schema from scratch at any time.

Note: Generally, we use migrations for changes to the database schema, not the data in a database; ie, to modify the tables in the database, not to modify the records in the database.

There are a few terminal commands that will generate a migration. These include:

```text
rails generate model Kitten
rails generate migration add_species_to_kitten
```

Migrations are stored in the db/migrate directory and the filenames are prefixed with a timestamp representing the actual time the migration file was generated, eg: **20160706022128\_create\_kittens.rb**. Rails runs migrations according to the order of their timestamps, so it's important that you do NOT edit the filename of a migration.

We most commonly use migrations to:

1. Create a table in our schema;
2. Modify a table in our schema.

### Migrations to create a table {#migrations-to-create-a-table}

Creating a model using `rails generate model` will create a migration for creating the table for that model:

```bash
rails generate model Kitten
# => create    db/migrate/20160706031227_create_kittens.rb
```

The migration file will look something like this:

```ruby
class CreateKittens < ActiveRecord::Migration
  def change
    create_table :kittens do |t|
​
      t.timestamps null: false
    end
  end
end
```

In its most basic form, we would then add columns to that table...

```ruby
class CreateKittens < ActiveRecord::Migration
  def change
    create_table :kittens do |t|
      t.string :name
      t.string :name
      t.integer :age
      t.timestamps null: false
    end
  end
end
```

Once we have filled out the migration, we run the migrations - this will run all migrations that have yet to be run, in order according to their timestamps:

```text
rails db:migrate
```

It's important to check that the migration was successful - ideally, the terminal response should be something like this:

```bash
== 20160706031227 CreateKittens: migrating ====================================
-- create_table(:kittens)
```

If not, there was a problem with your migration! Read the terminal response and try again.

## Homework

* Create your own version of CRUD system

  


