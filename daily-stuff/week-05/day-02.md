# Day 02

What we covered today:

* Ruby on Rails - Basic Project Setup \(with database\)

### Warmup {#warmup}

* Robot factory - Ruby​

### Classwork {#classwork}

* ​Movie-search
* ​planets-db

## Ruby on Rails - Basic Project Setup \(with database\) {#ruby-on-rails-basic-project-setup-with-database}

Treat this as a really rough guide, and definitely don't always follow it - you'll figure out your approach soon. This is a basic approach you might follow when setting up a new Rails project:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Step</th>
      <th style="text-align:left">What</th>
      <th style="text-align:left">Where</th>
      <th style="text-align:left">How</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Planning</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Pen & paper</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Create a new Rails app</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left"><code>rails new kitten_party</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Move into the new app's dir</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left"><code>cd kitten_party</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Add development Gems</td>
      <td style="text-align:left">/Gemfile</td>
      <td style="text-align:left"><code>gem &quot;pry-rails&quot;</code> 
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Bundle Gems</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left"><code>bundle</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">Create database</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left"><code>rails db:create</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">Create migration file</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left"><code>rails generate migration create_kittens</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">Open atom</td>
      <td style="text-align:left">Atom</td>
      <td style="text-align:left"><code>atom .</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">Go to db folder</td>
      <td style="text-align:left">Atom</td>
      <td style="text-align:left">Go to app -> db -> migrate -> 20181009011230_create_kittens.rb</td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">Add columns to migration file</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left">
        <p>An example table:</p>
        <p></p>
        <p><code>def change </code>
        </p>
        <p><code> create_table :kittens do |t|</code>
        </p>
        <p><code>  t.string :name </code>
        </p>
        <p><code>  t.text :image </code>
        </p>
        <p><code>  t.integer :roundness</code>
        </p>
        <p><code> end</code>
        </p>
        <p><code>end</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">11</td>
      <td style="text-align:left">Run migration</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left"><code>rails db:migrate</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Check schema.rb</td>
      <td style="text-align:left">Atom</td>
      <td style="text-align:left">Go to app -> db -> schema.rb and check the structure is the same as your
        create_kittens.rb</td>
    </tr>
    <tr>
      <td style="text-align:left">13</td>
      <td style="text-align:left">Check migration status</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left"><code>rails db:migrate:status</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">14</td>
      <td style="text-align:left">Edit migration as required</td>
      <td style="text-align:left">/db/migrate/[your_migration].rb</td>
      <td style="text-align:left">Add timestamps, more columns, etc if required.</td>
    </tr>
    <tr>
      <td style="text-align:left">15*</td>
      <td style="text-align:left">Create first controller</td>
      <td style="text-align:left">Terminal</td>
      <td style="text-align:left"><code>We will do it manually for now<br />(go to the controller folder and create a controller file called &quot;kittens_controller.rb&quot;)</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">16</td>
      <td style="text-align:left">Add methods to the controller</td>
      <td style="text-align:left">/app/controllers/kittens_controller.rb</td>
      <td style="text-align:left">Add methods for each action</td>
    </tr>
    <tr>
      <td style="text-align:left">17</td>
      <td style="text-align:left">Add views for your actions</td>
      <td style="text-align:left">/app/views/kittens/</td>
      <td style="text-align:left">Add an [action].html.erb file for each action that has an associated view</td>
    </tr>
    <tr>
      <td style="text-align:left">18</td>
      <td style="text-align:left">Configure routes</td>
      <td style="text-align:left">/config/routes.rb</td>
      <td style="text-align:left"><code>root :to =&gt; &quot;kittens#index&quot;</code>  <code>resources :kittens</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">19</td>
      <td style="text-align:left">Repeat for other models</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Repeat steps 7-19 for each model</td>
    </tr>
  </tbody>
</table>\* You can specify the actions for which you would like Rails to create views and methods when generating the controller by adding them to the end of the command - eg `rails generate controller Kittens index show edit new`. This will create those views, and the placeholder methods in your controller, but it also generates a bunch of routes that you will probably want to delete.

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

  


