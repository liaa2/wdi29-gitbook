# Day 05

What we covered today:

* Three.js contd
* Advanced JS Async

### Codealongs <a id="codealongs"></a>

* ​[Three.js 2​](https://github.com/textchimp/wdi-29/tree/master/week11/3d-graphics-threejs)
* [​​Advanced JS Async​](https://github.com/textchimp/wdi-29/tree/master/week11/promises)

## Advanced JS Async <a id="algorithms"></a>

### _The Fetch API_ <a id="the-fetch-api"></a>

The Fetch API provides a `fetch()` method defined on the window object, which you can use to perform requests. This method returns a Promise that you can use to retrieve the response of the request.

The fetch method only has one mandatory argument, which is the URL of the resource you wish to fetch. A very basic example would look something like the following. This fetches the top five posts from `r/javascript on Reddit`:

```javascript
fetch('https://www.reddit.com/r/javascript/top/.json?limit=5')
.then(res => console.log(res));
```

If you inspect the response in your browser’s console, you should see a `Response` object with several properties:

```javascript
{
  body: ReadableStream
  bodyUsed: false
  headers: Headers {}
  ok: true
  redirected: false
  status: 200
  statusText: ""
  type: "cors"
  url: "https://www.reddit.com/top/.json?count=5"
}
```

It seems that the request was successful, but where are our top five posts? Let’s find out.

### _Loading JSON_ <a id="loading-json"></a>

We can’t block the user interface waiting until the request finishes. That’s why `fetch()` returns a Promise, an object which represents a future result. In the above example, we’re using the then method to wait for the server’s response and log it to the console.

Now let’s see how we can extract the JSON payload from that response once the request completes:

```javascript
fetch('https://www.reddit.com/r/javascript/top/.json?limit=5')
.then(res => res.json())
.then(json => console.log(json));
```

We start the request by calling `fetch()`. When the promise is fulfilled, it returns a Response object, which exposes a json method. Within the first `then()` we can call this json method to return the response body as JSON.

However, the json method also returns a promise, which means we need to chain on another `then()`, before the JSON response is logged to the console.

And why does `json()` return a promise? Because HTTP allows you to stream content to the client chunk by chunk, so even if the browser receives a response from the server, the content body might not all be there yet!

### _Async … Await_ <a id="async-await"></a>

The `.then()` syntax is nice, but a more concise way to process promises in 2018 is using async … `await` — a new syntax introduced by ES2017. Using async `await` means that we can mark a function as async, then wait for the promise to complete with the await keyword, and access the result as a normal object. Async functions are supported in all modern browsers

Here’s what the above example would look like \(slightly expanded\) using async … await:

```javascript
async function fetchTopFive(sub) {
  const URL = `https://www.reddit.com/r/${sub}/top/.json?limit=5`;
  const fetchResult = fetch(URL)
  const response = await fetchResult;
  const jsonData = await response.json();
  console.log(jsonData);
}
​
fetchTopFive('javascript');
```

Not much has changed. Apart from the fact that we’ve created an async function, to which we’re passing the name of the subreddit, we’re now awaiting the result of calling `fetch()`, then using await again to retrieve the `JSON` from the response.

That’s the basic workflow, but things involving remote services doesn’t always go smoothly.

### _Handling Errors_ <a id="handling-errors"></a>

Imagine we ask the server for a non-existing resource or a resource that requires authorization. With `fetch()`, you must handle application-level errors, like 404 responses, inside the normal flow. As we saw previously, fetch\(\) returns a Response object with an ok property. If response.ok is true, the response status code lies within the 200 range:

```javascript
async function fetchTopFive(sub) {
  const URL = `http://httpstat.us/404`; // Will return a 404
  const fetchResult = fetch(URL)
  const response = await fetchResult;
  if (response.ok) {
    const jsonData = await response.json();
    console.log(jsonData);
  } else {
    throw Error(response.statusText);
  }
}
​
fetchTopFive('javascript');
```

The meaning of a response code from the server varies from API to API, and oftentimes checking response.ok might not be enough. For example, some APIs will return a 200 response even if your API key is invalid. Always read the API documentation!

To handle a network failure, use a try … catch block:

```javascript
async function fetchTopFive(sub) {
  const URL = `https://www.reddit.com/r/${sub}/top/.json?limit=5`;
  try {
    const fetchResult = fetch(URL)
    const response = await fetchResult;
    const jsonData = await response.json();
    console.log(jsonData);
  } catch(e){
    throw Error(e);
  }
}
​
fetchTopFive('javvascript'); // Notice the incorrect spelling
```

The code inside the catch block will run only when a network error occurs.

You’ve learned the basics of making requests and reading responses. Now let’s customize the request further.

### _Change The Request Method And Headers_ <a id="change-the-request-method-and-headers"></a>

Looking at the example above, you might be wondering why you couldn’t just use one of the existing `XMLHttpRequest` wrappers. The reason is that there’s more the fetch API offers you than just the `fetch()` method.

While you must use the same instance of `XMLHttpRequest` to perform the request and retrieve the response, the fetch API lets you configure request objects explicitly.

For example, if you need to change how `fetch()` makes a request \(e.g. to configure the request method\) you can pass a Request object to the `fetch()` function. The first argument to the Request constructor is the request URL, and the second argument is an option object that configures the request:

```javascript
async function fetchTopFive(sub) {
  const URL = `https://www.reddit.com/r/${sub}/top/.json?limit=5`;
  try {
    const fetchResult = fetch(
      new Request(URL, { method: 'GET', cache: 'reload' })
    );
    const response = await fetchResult;
    const jsonData = await response.json();
    console.log(jsonData);
  } catch(e){
    throw Error(e);
  }
}
​
fetchTopFive('javascript');
```

Here, we specified the request method and asked it never to cache the response.

You can change the request headers by assigning a `Headers` object to the request `headers` field. Here’s how to ask for `JSON` content only with the `'Accept'` header:

```javascript
const headers = new Headers();
headers.append('Accept', 'application/json');
const request = new Request(URL, { method: 'GET', cache: 'reload', headers: headers });

```

You can create a new request from an old one to tweak it for a different use case. For example, you can create a `POST` request from a `GET` request to the same resource. Here’s an example:

```javascript
const postReq = new Request(request, { method: 'POST' });
```

You also can access the response headers, but keep in mind that they’re read-only values.

```javascript
fetch(request).then(response => console.log(response.headers));
```

`Request` and `Response` follow the HTTP specification closely; you should recognize them if you’ve ever used a server-side language. If you’re interested in finding out more, you can read all about them on the [Fetch API page on MDN.](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)​  


### Further Reading <a id="further-reading"></a>

* ​[Fetch API MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)​
* ​[Introduction to Fetch API](https://www.sitepoint.com/introduction-to-the-fetch-api/)​
* ​[Promises MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)​
* ​[Promises Introduction](https://developers.google.com/web/fundamentals/primers/promises)​



