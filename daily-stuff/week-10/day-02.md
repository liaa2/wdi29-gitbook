# Day 02

What we covered today:

* Frontend Auth with JWT

#### Warmup <a id="warmup"></a>

* ​[Happy Numbers​](https://github.com/liaa2/wdi29-homework/tree/master/warmups/week10/day02_happy_numbers)

#### Classwork <a id="classwork"></a>

* ​[Codealong​](https://github.com/textchimp/wdi-29/tree/master/week10/burning-airlines-rails-vue)

## Authentication using JWT <a id="authentication-using-jwt"></a>

### Rails Knock gem <a id="rails-knock-gem"></a>

Knock is an authentication solution for Rails API-only application based on JSON Web Tokens.

​[Knock](https://github.com/nsarno/knock)​

#### Why should I use this? <a id="why-should-i-use-this"></a>

* `It's lightweight.`
* `It's tailored for Rails API-only application.`
* `It's stateless.`
* `It works out of the box with Auth0.`

#### Using Knock <a id="using-knock"></a>

Add the gem to your Gemfile

```bash
gem 'knock'
```

Run bundle

```bash
bundle
```

Run the install generator

```bash
rails g knock:install
```

This will create the following initializer `config/initializers/knock.rb`. This file contains all the information about the existing configuration options.

Run the following command to provide a way for users to sign in.

```bash
rails g knock:token_controller user
```

This will generate the controller `user_token_controller.rb` and add the required route to your `config/routes.rb file`.

### Usage <a id="usage"></a>

Include the Knock::Authenticable module in your ApplicationController

```ruby
class ApplicationController < ActionController::API
  include Knock::Authenticable
end
```

Resources can now be secured by calling authenticate\_user as a before\_action inside your controllers

```ruby
class FlightsController < ApplicationController
​
  before_action :authenticate_user, except: [:index]
  
  def index
    ...
  end
​
  def search
    ...
  end
​
  def show
    ...
  end   
​
end

```

You can access the current user in your controller with current\_user.

```ruby
def index
  if current_user
    # do something
  else
    # do something else
  end
end
```

_Note: the authenticate\_user method uses the current\_user method. Overwriting current\_user may cause unexpected behaviour._

### What is JSON Web Token? <a id="what-is-json-web-token"></a>

JSON Web Token \(JWT\) is an open standard \(RFC 7519\) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret \(with the HMAC algorithm\) or a public/private key pair using RSA or ECDSA.

### When should you use JSON Web Tokens? <a id="when-should-you-use-json-web-tokens"></a>

Here are some scenarios where JSON Web Tokens are useful:

* **Authorization:** This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token. Single Sign On is a feature that widely uses JWT nowadays, because of its small overhead and its ability to be easily used across different domains.
* **Information Exchange:** JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are. Additionally, as the signature is calculated using the header and the payload, you can also verify that the content hasn't been tampered with.

### What is the JSON Web Token structure? <a id="what-is-the-json-web-token-structure"></a>

In its compact form, JSON Web Tokens consist of three parts separated by dots \(.\), which are:

* `Header`
* `Payload`
* `Signature`

Therefore, a JWT typically looks like the following.

`xxxxx.yyyyy.zzzzz`

### Let's break down the different parts. <a id="lets-break-down-the-different-parts"></a>

**Header**

The header typically consists of two parts: the type of the token, which is JWT, and the hashing algorithm being used, such as HMAC SHA256 or RSA.

For example:

```javascript
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Then, this JSON is Base64Url encoded to form the first part of the JWT.

**Payload**

The second part of the token is the payload, which contains the claims. Claims are statements about an entity \(typically, the user\) and additional data.

An example payload could be:

```javascript
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

The payload is then Base64Url encoded to form the second part of the JSON Web Token.

**Signature**

To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

```javascript
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

**Putting all together**

The output is three Base64-URL strings separated by dots that can be easily passed in HTML and HTTP environments, while being more compact when compared to XML-based standards such as SAML.

**How do JSON Web Tokens work?**

In authentication, when the user successfully logs in using their credentials, a JSON Web Token will be returned. Since tokens are credentials, great care must be taken to prevent security issues. In general, you should not keep tokens longer than required.

Whenever the user wants to access a protected route or resource, the user agent should send the JWT, typically in the Authorization header using the Bearer schema. The content of the header should look like the following:

```javascript
Authorization: Bearer <token>
​
// ./src/components/Login.vue
​
// This header-setting line also appears in App.vue, but that's too late for
// us here; it will already have run by the time we perform this login -
// so we have to set the header again here
axios.defaults.headers.common['Authorization'] = `Bearer ${response.data.jwt}`;
```

This can be, in certain cases, a stateless authorization mechanism. The server's protected routes will check for a valid JWT in the `Authorization` header, and if it's present, the user will be allowed to access protected resources. If the JWT contains the necessary data, the need to query the database for certain operations may be reduced, though this may not always be the case.

If the token is sent in the `Authorization` header, Cross-Origin Resource Sharing \(CORS\) won't be an issue as it doesn't use cookies.

#### Homework: as many of the following as you can manage: <a id="homework"></a>

1. FlightDetails: show the correct colour for reserved seats by checking each seat against the `reservations` data
2. FlightDetails: add the ability to reserve a seat \(add a click handler to eat seat div, which makes a `POST` request to a new Rails route like `/booking`, passing as params the `row` and `col` of the clicked seat, and the flight ID; make sure to use `current_user` in the Rails controller to get the logged-in user's ID\)
3. Add a nav bar to the app with Login/Logout links, depending on whether the user is already logged in or not
4. Learnyounode: try another few exercises and bring your questions/issues in tomorrow morning
5. Learnyounode: COMPETITION: draw a diagram of the flow of arguments between functions in the Make It Modular exercise. Best diagram wins the respect and gratitude of the class, and a worthless prize like a sticker or something



**Further Reading:**

* ​[Ruby on Rails and JWT+Knock](https://engineering.musefind.com/building-a-simple-token-based-authorization-api-with-rails-a5c181b83e02)​
* ​[5 Easy Steps to Understanding JWT](https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec)​
* ​[JWT: The Complete Guide to JSON Web Tokens](https://blog.angular-university.io/angular-jwt/)​
* ​[Understanding JWT](http://polyglot.ninja/understanding-jwt-json-web-tokens/)​
* ​[Rails API + JWT auth + VueJS SPA](https://blog.usejournal.com/rails-api-jwt-auth-vuejs-spa-eb4cf740a3ae)​

