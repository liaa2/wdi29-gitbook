# Day 05

What we covered today:

* Ruby on Rails - User login:
  * Ruby on Rails - Validations

### Warmup {#warmup}

* [​Luhn Numbers](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week05/day05_luhn_numbers)

### Classwork {#classwork}

* ​[Tunr​ \(continued\)](https://github.com/textchimp/wdi-29/tree/master/week5/tunr-db-wdi29)

## Validations {#validations}

### Interlude - front-end v back-end validations {#interlude-front-end-v-back-end-validations}

Validations in a full-stack web app basically fall into two categories - front-end validations and back-end validations. This part of the GitBook only deals with the latter. Front-end validations are client-side validations which prevent users from performing certain actions in a form _before_ anything is posted back to the application - they submit a user from entering certain information in a form, or submitting a form with/out certain attributes, like putting alphabetic characters in a number field, or exceeding a character limit for a text field, or leaving a required field blank.

Front-end validations are great for user experience and performance, but they're vulnerable to circumvention - we usually also want back-end validations.

### Active Record validations {#active-record-validations}

As with virtually every problem in the universe, Active Record has a solution. Instead of trying to create our own validations for data that is getting submitted to a database, lets see what solutions Active Record has.

These validations go within the model against which the validation needs to be performed \(for example, validations relating to the User model should go in app/models/user.rb\).

#### _Why should we use validations?_ {#why-should-we-use-validations}

Because the internet is a scary, scary world and there are scary, scary things that people will try and put in your database.

#### _When do validations take place?_ {#when-do-validations-take-place}

Active Record Validations occur when any of the following methods take place:

* `create`
* `create!`
* `save`
* `save!`
* `update`
* `update!`

If you want to skip validations, they won't take place when using the following methods.

* `decrement!`
* `decrement_counter`
* `increment!`
* `increment_counter`
* `toggle!`
* `touch`
* `update_all`
* `update_attribute`
* `update_column`
* `update_columns`
* `update_counters`

You can also pass `:validate => false` to the save method.

#### _How to test validity?_ {#how-to-test-validity}

There are methods!

* `valid?`
* `invalid?`

If a model is invalid, you can access the errors easily as well. These will be in the `.errors.messages`.

#### _Alright, enough of this. Now for some Validation Helpers_ {#alright-enough-of-this-now-for-some-validation-helpers}

```ruby
class User < ApplicationRecord
  has_many :books
  validates :column_name, :key => value
end
```

**acceptance**

This method validates that a checkbox on the user interface was checked when a form was submitted. This is how terms of service are accepted for example.

```ruby
validates :terms_of_service, acceptance: true
​
# It defaults to "1", if you want to accept something else
​
validates :terms_of_service, acceptance = { :accept => "yes" }
```

**validates\_associated**

If you have associations, you can validate those associations by using validate associated.

```ruby
validates_associated :column_name
```

Don't do this on both sides of the associations! It will cause an infinite loop.

**confirmation**

You should use this helper if you have two text fields that should receive exactly the same content. This validation creates a virtual attribute whose name is the name of the field but with "\_confirmation" at the end.

```ruby
validates :email, :confirmation => true
​
# This should always work with a nil check as well
​
validates :email_confirmation, :presence => true
```

**exclusion**

This helper validates that the attributes' values are not included in a given set. It requires an :in option that receives the set of values that cannot be included, as well as an optional :message option to show how you can include the attribute's value.

```ruby
validates :subdomain, :exclusion => {
  :in => [ "www", "us", "ca", "jp" ],
  :message => "%{ value } is reserved. "
}
​
# Notice the interpolation with value, that takes the excluded value
```

**format**

This helper validates the attributes' values by testing whether they match a given regular expression, which is specified using the :with option.

```ruby
validates :legacy_code, format: {
  :with => /\A[a-zA-Z]+\z/,
  :message => "only allows letters"
}
```

Alternatively, you can require that the specified attribute does not match the regular expression by using the :without option.

**length**

This helper validates the length of the attributes' values. It provides a variety of options, so you can specify length constraints in different ways:

```ruby
validates :name, length: { minimum: 2 }
validates :bio, length: { maximum: 500 }
validates :password, length: { in: 6..20 }
validates :registration_number, length: { is: 6 }
```

**numericality**

This helper works with numericality.

```ruby
validates :count, numericality: { :only_integer => true }
```

Besides `:only_integer`, you can also work with the following:

* `:greater_than` - Specifies the value must be greater than the supplied value. The default error message for this option is "must be greater than %{count}".
* `:greater_than_or_equal_to` - Specifies the value must be greater than or equal to the supplied value. The default error message for this option is "must be greater than or equal to %{count}".
* `:equal_to` - Specifies the value must be equal to the supplied value. The default error message for this option is "must be equal to %{count}".
* `:less_than` - Specifies the value must be less than the supplied value. The default error message for this option is "must be less than %{count}".
* `:less_than_or_equal_to` - Specifies the value must be less than or equal the supplied value. The default error message for this option is "must be less than or equal to %{count}".
* `:odd` - Specifies the value must be an odd number if set to true. The default error message for this option is "must be odd".
* `:even` - Specifies the value must be an even number if set to true. The default error message for this option is "must be even".

**presence**

Checks whether the value of a particular set of attributes is nil or an empty string.

```ruby
validates :email, :presence => true
```

**absence**

Does the opposite or `:presence`, makes sure it is not there.

```ruby
validates :email, :absence => true
```

**uniqueness**

Makes sure there is only one of these columns with this particular value.

```ruby
validates :email, uniqueness: true
```

#### _Working with Validation Errors_ {#working-with-validation-errors}

Taking an invalid person as example...

```bash
person.valid?
# Returns false
​
person.errors
 # Returns an instance of the class ActiveModel::Errors containing all errors. Each 
 # key is the attribute name and the value is an array of strings with all errors.
​
person.errors.messages
# Returns all of the messages associated
```

### _Ruby on Rails - Validations - Further Readings_ {#ruby-on-rails-validations-further-readings}

* ​[Rails Guides - Active Record Validations](http://guides.rubyonrails.org/v4.2/active_record_validations.html)​

###   {#ruby-on-rails-validations-further-readings}

