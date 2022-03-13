# APIs and Asynchronous JS

An API is a tool that connects your program with somebody else's program. Examples:

* A server exposing certain 'endpoints' to give users access to parts of their data.
* Pre-written code, such as JS DOM methods and other internal methods.
* 3rd party packages: [see web APIs list here](https://developer.mozilla.org/en-US/docs/Web/API).

## Clients and Servers

There is a request and response cycle going on between the two:

* A client is any device that makes requests over the internet to receive data. Clients request a resource, such as a document or image.
* A server accepts requests from clients and responds back with either the resource or an error message.

## Server Responses Examples

* 200 OK
* 403 Forbidden
* 404 Not Found
* 500 Internal Server Error

JSON stands for JS Object Notation. It is the language of data on the web, and it is user to transfer data from one place to another. The contents of a .json file are either an object, or an array of objects.

## Basic Fetch Request

`Fetch` is asking for data from a server in the paramenter link. `.then` returns the response we receive from the json file coming from the server, and then turns that data into JS.

The method `.then` is executed at the end of a script, even if it sits at the beginning.

```js
fetch("https://dog.ceo/api/breeds/image/random")
    .then(response => response.json())
    .then(data => console.log(data))
```

## HTTP Requests

HTTP (Hypertext Transfer Protocol) is a protocol for determining how Hypertext should be transferred over the internet.

* FTP is short for File Transfer Protocol.
* SMTP is short or Simple Mail Transfer Protocol.

There are different components to a request:

* The client sends the request to a path/URL. This is the address where a resource is, and it points to an IP address. It is divided into a base URL that doesn't change, and an endpoint that points to the resource we need. URLs can be nested with their own parameters, usually numeric IDs such as bikes/123/reviews/5, and these variables act as a placeholder for the real value.
* The request must include a method, such as GET, POST, PUT, DELETE. Respectively they: get data, add new data, update existing data, delete existing data.
* A body, that is only included with a POST or PUT request.
* A header with meta information about the request.

Fetch defaults to GET, but it takes other methods as a paramenter.

```js
fetch("https://apis.scrimba.com/jsonplaceholder/todos", {method: "POST"})
```

## Using fetch to loop through an API's data and place it in a container

```js
fetch("https://apis.scrimba.com/jsonplaceholder/posts")
    .then(res => res.json())
    .then(data => {
        const postsArr = data.slice(0, 5)
        let html = ""
        for (let post of postsArr) {
            html += `
                <h3>${post.title}</h3>
                <p>${post.body}</p>
                <hr />
            `
        }
        document.getElementById("blog-list").innerHTML = html
    })
```

## Fetch Request with POST method and both body and header

The header serves the purpose of telling the server that the body content is going to be a json file format. The body just needs to be converted to a string.

```js
fetch("https://apis.scrimba.com/jsonplaceholder/todos", {
    method: "POST",
    body: JSON.stringify({
        title: "Buy Milk",
        completed: false
    }),
    headers: {
        "Content-Type": "application/json"
    }
})
    .then(res => res.json())
    .then(data => console.log(data))
```

## REST

REST stands for Representational State Transfer. It is a design pattern that provides a standard way for clients and server to communicate. A RESTful API on a server allows for any client, whatever the device, to ask for data in JSON format, that will then be rendered by the device. If the server builds and HTML page instead, and returns that to the client, not all clients would be able to read it.

With a RESTful API, Servers do not keep a record of the requests received by clients. The interaction by the two is erased once the response is sent. This is called a stateless server.

RESTful API categories should only be a single name of the collection of items they include. This is by design. The verb and action is specified in the method we use.

APIs have custom routes for their nested items, so check the documentation for any API calls you might need.

## Query Strings

Query Strings are a way to filter the results returned by an API. See examples.

`/bikes?type=road&brand=trek&color=blue
/bikeracks?available=true
/bikeracks?brand=thule&numBikes=4`

`&type` and everything afterwards is the query string of the URL. It will create an object with all the inserted parameters.

roma 3169069

## Asynchronous JS

Async JS is code that can run out of order. An operation can start anytime and finish later, allowing other code to be executed in the meantime.

JS is a single-threaded language that can only run one command at a time. It isn't truly asynchronous, but rather it uses callback mechanisms to change the orders programs are run in.

When working with APIs, there is no guarantee when the server will give return a response, so callbacks are used instead.

## Callback functions

Functions are first-class objects in JS. This means they can be used as values when declaring a variable, and they can be used as a parameter with other functions.

When a function takes another functions as a parameter, the former is a higher order function, and the latter a callback function.

`setTimeout` is an example of a higher order function using a callback function.

```js
function callback() {
    console.log("I finally ran!")
}

setTimeout(callback, 2000)
```

## Promises

A fetch request always returns a promise object.

A promise occurs whenever an action is asynchronous. Instead of returning a value or a reason for failure immediately, a promise to do so later is returned instead. A promise can either be pending, fulfilled, or rejected.

Promises can be chained like methods, as long as parameters keep being returned.

```js
fetch("https://apis.scrimba.com/bored/api/activity")
    .then(function(res) {
        return "Hello"
    })
    .then(function(whatever) {
        console.log(whatever)
        return "World"
    })
    .then(function(another) {
        console.log(another)
    })
```

## Async/Await

Async and Await use a different syntax but work the same as Fetch and .then. The two functions below are equivalent.

```js
async function handleClick() {
    const res = await fetch("https://apis.scrimba.com/deckofcards/api/deck/new/shuffle/")
    const data = await res.json()
    remainingText.textContent = `Remaining cards: ${data.remaining}`
    deckId = data.deck_id
    console.log(deckId)
}

function handleClick() {
    fetch("https://apis.scrimba.com/deckofcards/api/deck/new/shuffle/")
        .then(res => res.json())
        .then(data => {
            remainingText.textContent = `Remaining cards: ${data.remaining}`
            deckId = data.deck_id
            console.log(deckId)
        })
}
```

Other example:

```js
async function getPhotos() {
    let response = await fetch("photos.json")
    let photos = await response.json()
    return photos
}

getPhotos().then(photos => {
    let myPhotosHtml = photos.map(photo => {
        return `<img src="https://picsum.photos/id/${photo.id}/100/100" alt="${photo.title}"/>`
    }).join('')
    console.log(myPhotosHtml)
    
    document.body.innerHTML = `<div class="my-photos">${myPhotosHtml}</div>`
})
```

## Rejected Promises and Error Handling

A fulfilled promise is a happy path. Should this not happen, the rejected promise must be handled. This happens whenever an error occurs inside a .then() object. Use .`catch` to give a default output in case something goes wrong.

`throw` will ensure an error message is thrown to `catch` if the result is not okay.

```js
fetch("api url")
    .then(res => {
        if (!res.ok) {
            throw Error("Something went wrong")
        }
        return res.json()
    })
    .then(data => {
        document.body.style.backgroundImage = `background image url)`
    })
    .catch(err => {
        document.body.style.backgroundImage = `default background image url)`
    })
```

## Misc

A sync system is like a baton pass. Async is a regular marathon.
