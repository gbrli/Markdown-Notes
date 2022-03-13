# JS Bootcamp II

## DOM

* querySelector will get the first element of that type.
* append and prepend can be used both.
* the callback function in an event listener with event allows us to use methods such as event.target in the function body

## Classes

Classes and constructor functions in JS work the same way.

```js
class Film {
    constructor(id, title,director, releaseYear, genres = []) {
        this.id = id;
        this.title = title;
        this.director = director;
        this.releaseYear = releaseYear;
        this.genres = genres;
    }
       
    addGenre(genre) {
        this.genres = [...this.genres, genre];
    }

    getFilmTitle() {
        return `Film: ${this.title}`
    }
}
```

Extends makes child classes. Super will reference the parent class and allow to access methods and values from it.

```js
class Product {
  constructor(name, price, discountable) {
    this.name = name;
    this.price = price;
    this.discountable = discountable;  
  }  
  
  isDiscountable() {
    return this.discountable;  
  }
}

class SaleProduct extends Product {
  constructor(name, price, discountable, percentOff) {
     super(name, price, discountable);
     this.percentOff = percentOff; 
  }  
  
  getSalePrice() {
     if (super.isDiscountable()) {
       return this.price * ((100 - this.percentOff) / 100);
     } else {
        return `${this.name} is not eligible for a discount`;
     }
  }
}

const saleProduct1 = new SaleProduct("Coffee Maker", 99, false, 20);
console.log(saleProduct1.getSalePrice());
```

A getter allows us to access properties in an object. A setter allows users to change or mutate the properties in an object, while ensuring that the value set is a valid type. Variables with an underscore _ indicate their importance and should not be changed.

```js
get price() {
    return this._price;
  }

set price(price) {
   if (typeof price !== "number") {
     return this._price;
   } else {
     this._price = price;
   }
 }
}
```

## Async

Code that needs to be executed after a function needs to be inside its callback. Callback hell happens when you have async functions waiting for another one to execute, all in one long chain of callbacks. Inversion of control happens in callback hell: when you have multiple callback-based functions that are depenendant on each other's results to resolve succesfully, the callbacks are in control of the program. You are not.

Promise objects are used to write async code without getting into callback hell. Promises can invoke the methods then and catch.

A promise can have three states: pending, fulfilled or rejected. Resolve and reject will change the promise state to fulfilled or rejected respectively.

When resolve is called, the code executes the function passed to the then() method. When reject is called it executes the function passed to the catch() method. finally() is used to run code after a promise runs, successfully or not.

```js
const promise = new Promise((resolve, reject) => {
    navigator.geolocation.getCurrentPosition(position => {
        resolve(position)
    }, error => {
        reject(error)
    })
})

promise
    .then(position => console.log(position))
    .catch(error => console.log(error))
    .finally(() => console.log('done'))
```

## APIs

APIs are a means for software to communicate with other software - in other words, a helpful service. It doesn't have to be third party: the window object is an API as well.

A REST API is a third party API. AJAX requests (meaning network requests) are made to them with HTTP methods.

* Create - POST
* Read - GET
* Update - PUT/PATCH
* Delete - DELETE

Adding data to an API with a POST request:

```js
fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: {
    "Content-Type": "application/json"
    },
    body: JSON.stringify(blogPost)
})
    .then(response => response.json())
    .then(data => console.log(data.title));
```

Getting data from an API including checking errors:

```js
fetch("https://jsonplaceholder.typicode.com/users/3")
.then(response => {
    if (!response.ok) {
        throw new Error(response.status);
    }
    return response.json();
})
.then(person => {
    console.log(`${person.name} works for ${person.company.name}`);
})
.catch(err =>  console.log(err));
```

Async functions always return a promise. Await waits for the promise to resolve, and then uses the value.

```js
async function getPost() {
   const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');  
   const data = await response.json();
   console.log(data);
}

getPost();

// catching errors with try/catch in async/await
async function getUser() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users/3');
    if (!response.ok) {
      throw new Error(response.status);
    }
    const person = await response.json();
    console.log(person);    
  }
    catch (error) {
      console.log(error);
  }
}

getUser()
```

## Modules

Modules allow us to split an application into multiple files. This ensures a separation of concerns and it is what frameworks and libraries are based on.

```js
<script src="index.js" type="module"></script>
// component
export default function getUser() {
  return {
    name: "Clementine Bauch", 
    company: "Romaguera-Jacobson"
  }
}

// app
import getUser from './utils/getUser.js';

class App {
  constructor() {
    this.render();
  } 
  
  render() {
    const user = getUser();
    console.log(user);
    document.getElementById('root').innerHTML = `
      <div>${user.name} works for ${user.company}</div>
    `
  }
}

new App();
```

## State

All frameworks work around the concept of state in JS. State is the data that is managed by an application. The state of an app should be the only source of truth.

```js
class App {
    // app constructor manages state
  constructor() {
    this.state = {
       isAuth: false,
       error: ''  
    };  
    // runs functions      
    this.checkAuth();
    this.render();
}
    // updates state based on bool value
  checkAuth() {
    const user = false;
    if (user) {
      this.state = { ...this.state, isAuth: true };
    } else {
      this.state = { ...this.state, error: "You must sign in!" };
    }
}
// renders the state in html
  render() {
    const { isAuth, error } = this.state; 
      
    document.getElementById("root").innerHTML = `
      <div style="color: ${error && 'red'}">
        ${isAuth ? 'Welcome back!' : error}
      </div>
    `;
  }
}
// calls app function
new App();
```

A reducer function takes two parameters: the current state, and an action to be taken. A reducer is a pure function, meaning a function than returns the same output regardless of its input. State usually updates with an object and it is never updated directly. Reducers are the most powerful techniques to update state. Because state is immutable, we return a new object every time: type and count are arbitrary object parameters.

```js
// calc example
function counterReducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return { ...state, count: state.count + 1 }; 
    case 'DECREMENT':  
      return { ...state, count: state.count - 1 }; 
    default:
      return state;
  }  
}

counterReducer(0, { type: 'INCREMENT' }); // 1
const result = counterReducer(1, { type: 'DECREMENT' }); // 0
console.log(result === 0); // null

// user example
const initialUser = {
  name: 'Mark',
  email: 'mark@gmail.com'  
};

function userReducer(state, action) {
  switch (action.type) {
     case "CHANGE_NAME":
       return { ...state, name: action.payload.name };
     case "CHANGE_EMAIL":
       return { ...state, email: action.payload.email };
     default:
       return state; 
  }  
}

const result = userReducer(initialUser, { type: 'CHANGE_EMAIL', payload: { email: 'mark@compuserve.com' } });
console.log(result.email === 'mark@compuserve.com');
```

## This

They keyword `this` is a reference to an object, but the object can vary according to how a function is called. The value of `this` is dynamic in order to allow proper prototypal inheritance when using classes. The value can change in four different contexts:

1) in the global context (global object, undefined in strict mode)
2) as a method on an object (object on left side of dot)
3) as a constructor function or class constructor (the instance itself with new)
4) as a DOM event handler (the element itself)

```js
// global context: this function will return the window object. it will be undefined in strict mode.
function whatIsThis() {
    console.log(this)
}
```

```js
// as an object method: the function will return only the value within nums, because this only has access to that layer of data
const numbers = {
    name: 'blabla',
    nums: {
        one: '1',
        two: '2',
        sayNum() {
            console.log(`${this.name} ${this.one}`)
        }
    }
}
// returns undefined 1. the this keyword here refers to nums
numbers.nums.sayNum()
```

```js
// on a constructor function or class constructor. whenenever a new instance of a class is initiated, the this keyword will refer to its instance. so in this case this will always be what is stored in the Bob user.
class User {
  constructor(first, age) {
    this.first = first;
    this.age = age;  
  }  
  
  getAge() {
    console.log(`${this.first}'s age is ${this.age}`);  
  }
}

const user = new User('Bob', 24);
user.getAge();
```

```js
// as a DOM event handler, this will refer to event.target. here, this is equal to <button>
const button = document.createElement('button');
button.textContent = "Click";
document.body.appendChild(button);

button.addEventListener('click', function() {
  console.log(this);
})
```

## Call, Apply, Bind

Call will take two unrelated elements, an object and a function, and give the function access to `this` to refer to the object's values. Anything passed to `call` will become the context for `this`, and if a function requires parameters, they need to be added after the object in the function call.

`Apply` works the same way, but the arguments must be passed inside an array.

```js
// will log obj values
const user = {
  name: "Reed",
  title: "Programmer"  
}

function printBio(city, country) {
  console.log(`${this.name} is a ${this.title} in ${city}, ${country}`);
}
// adding multiple parameters after the obj
printBio.call(user, 'London', 'England')
// apply example
printBio.apply(user, ['London', 'England'])
```

`Bind` will provide `this` context to a function from an object. We can also bind the function directly inside the constructor.

```js
const user = {
  name: "Reed",
  title: "Programmer"
// alternative
  this.printUser = this.printUser.bind(this)
}
function printUser() {
  console.log(`${this.name} is a ${this.title}`);
}
const userDescription = printUser.bind(user);
}
```

Arrow functions don't create a new `this` binding, they always refer to the context a level above.
