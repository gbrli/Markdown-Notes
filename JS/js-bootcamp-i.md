# JS Bootcamp I

The advantage of using let and const is not running into problems with variable hoisting.

## Data Types

Data types can only be primitives or objects. String, number, boolean, undefined, null and symbol are primitive. Everything else is an object. Also all data types are either truthy or falsy.

Primitive values are always passed by value, meaning a new copy will be created in memory.

Objects types are passed by reference, meaning they point to the same place in memory an updating any of the two will change the same place in memory, so all of them will be affected.

Falsy values are false, 0, '', null, undefined, NaN.

There are two ways to change data types:

* Explicit type conversion, such as string(), boolean(), number()
* Implitic type conversion or coercion, such as console.log ('10' + 20) or the boolean in a conditional

Short-circuiting is using conditional operators for conditional rendering. && takes precedence over ||, but brackets go first always.

## Functions

A function can be returned by another function, but it must be stored in a variable to be executed.

A closure is an inner function inside an outer function's scope, and it has access to its variables. Closures are a property of functions alone. The value is only preserved when the inner function is called. Example countdown function:

```js
function countDown(num, step) {
    let countFromNum = num
    return function decrease() {
        countFromNum -= step
        return countFromNum
    }
}
const countingDown = countDown(20, 5);
console.log(countingDown());
```

Functions can take a default parameter. It's usually used when values are undefined in the body of a function. In this example decimalPlaces is always equal to 1 unless it's false.

```js
function convertTemperature(celsius, decimalPlaces = 1) {
    const fahrenheit = celsius * 1.8 + 32;
    return Number(fahrenheit.toFixed(decimalPlaces));
}
console.log(convertTemperature(21, 3));
console.log(convertTemperature(21, 0));
```

Arrow functions do not need a return keyword because they provide implicit return, meaning anything after the => keyword is returned. However, for readability purposes, the return keyword can be useful like in the callback arrow function below. Multiple lines should be in curly brackets.

```js
const countdown = (startingNumber, step) => {
  let countFromNum = startingNumber + step;
  return () => countFromNum -= step;
}
```

Instead of having one function with multiple actions, partial application allows us to split one function into different ones with single responsibilities. Callback functions can be used for this, and it improves readability. Partial application means that the first function is only applying part of its parameters at the beginning.

```js
// higher order function that takes a callback function as a parameter
function getData(baseUrl) {
  return function(route) { 
    return function(callback) {    
      fetch(`${baseUrl}${route}`)
        .then(response => response.json())
        .then(data => callback(data));  
    }     
  }  
}

// same function as above, but with arrow function syntax
const getData = baseUrl => route => callback =>  
      fetch(`${baseUrl}${route}`)
        .then(response => response.json())
        .then(data => callback(data));  

// get baseURL from API, then get the route for the posts
const getSocialMediaData = getData('https://jsonplaceholder.typicode.com');
const getSocialMediaPosts = getSocialMediaData('/posts');

// render all posts
getSocialMediaPosts(posts => {
  posts.forEach(post => console.log(post.title));  
});
```

## Objects

Properties can be added to objects in multiple ways. Delete can be used to remove a property.

```js
colors.newKey = "newValue"
colors[newKey2] = "newValue2"
delete colors.newKey
```

Object destructuring

```js
const {name, username, email} = user
// above is the same as below
const name = user.name
const username = user.username
const email = user.email
// destructuring a nested objects
const {details: { title, somethingElse }} = user
```

Merging objects and changing properties without modifying the original objects

```js
// ... and object.assign() do the same thing, but ... is more readable
const createdUser = { ...user, ...newUser, verified: false };
const createdUser2 = Object.assign({}, user, newUser, { verified: false }));
```

Iterating objects

```js
for (const key in obj) {
    console.log(key, obj[key])
}
```

`Object.keys, .values and .entries` return an array. Combining them with array methods is incredibly powerful when working with objects.

```js
const monthlyTotal = Object.values(monthlyExpenses).reduce(
    (acc, expense) => acc + expense, 0
);
```

Manipulating an object of objects and turning their data into a more manageable array

```js
const users = {
  '2345234': {
    name: "John",
    age: 29
  },
  '8798129': {
    name: "Jane",
    age: 42
  },
  '1092384': {
    name: "Fred",
    age: 17 
  }
};

const usersOver20 = Object.entries(users).reduce((acc, [id, user]) => {
  if (user.age > 20) {
    acc.push({ id, ...user});
  }  
  return acc;
}, []);
console.log(usersOver20);
```

## Maps

Maps are new object data types that have the following advatanges:

* Non-string can be used as keys
* Maps are in insertion order unlike objects
* Objects can be keys (in which case, use WeakMap)
* Data can be iterated easily
* Length of data is easy to get

```js
const userMap = new Map([
  ["name", "john"],
  ["verified", true]  
]);

// adding a new key value pair
map1.set('key', 'value');
// logging the map out
console.log([...map1.keys()])
// getting one item
console.log(place.get("name"))
```

The `this` keyword's main purpose is for functions within an object to reference object keys without having to refer constantly to the object name, because it might change. `userData.name` is replaced by `this.name`.

## Arrays

Finding index of element when we don't know the position:

```js
const nums = [1,2,3,4,5,6,7,8,9,0]
// returns index 3
nums.indexOf(4)
// not in array returns index -1
nums.indexOf(20)
// returns true, use this method instead
nums.includes(7)
```

Finding elements in a complex array:

```js
const temperatures = [
    { degrees: 69, isRecordTemp: false }, 
    { degrees: 82, isRecordTemp: false }, 
    { degrees: 73, isRecordTemp: false }, 
    { degrees: 64, isRecordTemp: false }
]

// return true if at least one value of isRecordTemp is true
const result = temperatures.some(temp => temp.isRecordTemp)
// return true if all values of isRecordTemp are true
const result = temperatures.every(temp => temp.isRecordTemp)
```

Higher methods like some and every use callback functions, usually with an arrow function.

```js
// map loops elements and return a new element. we can make modifications and add stuff
const newTemps = temperatures.map(temperature => 
temperature.degrees > 70 ? { ...temperature, isHigh: true } : temperature 
);
// forEach loops like map, but it modifies the initial array. use it to iterate
newTemps.forEach(temp => {
    if(temperature.isHigh) {
        console.log('Temp was high')
    }
})
```

`filter()` returns the elements that fulfill a condition.

`find()` returns only the first element that fulfills a condition.

`reduce()` iterates over the parameters and uses an accumulator as a reference. It returns the accumulator. **Reduce is incredibly powerful and can be used to recreate most array methods, because the majority of them are productions, meaning they take an array and change it to something else.**

**Instead of chaining multiple methods, one reduce is usually enough!**

```js
// will iterate object like map and accumulate the value of the price key of all object properties
menuItems.reduce((accumulator, menuItem) => {
    return accumulator =+ menuItem.price
}, 0)

// creating a new array thanks to [], only pushing values above 3
const numbers = [1, 2, 3, 4, 5, 6];
const ts = numbers.reduce((acc, num) => {
    num > 3 && acc.push(num)
    return acc
}, [])
```

Arrays are object types, so their values are passed by reference. In order to avoid mutating the existing array, different methods should be used.

`Push` changes the original array. `Concat` does not, `...` is even easier to use.

`Slice()` can be used with `...` when copying arrays.

```js
// findIndex returns the index of 5
// ... will copy from index 0 to where five is
// substitute it with cinque
// ... will put from five until end of array
const numbers = [1, 2, 3, 4, 5, 6];
const five = numbers.findIndex(num => num === 5)
const newNums = [...numbers.slice(0, five), "cinque", ...numbers.slice(five + 1)]
console.log(numbers)
console.log(newNums)
```

When destructuring an array, the rest operator can be used to split the rest into a different array.

```js
const nums = [1,2,3,4,5,6]
const [one, ...rest] = nums
console.log(one, rest)
```

## Sets

A set is a special object type in which each value is unique. Their order is preserved.

```js
const nums = new Set([1,2,3,4,5])
for (const num of nums) {
    console.log(num)
}
```

Get unique values only creating a new Set

```js
const customerDishes = [
  "Chicken Wings",
  "Fish Sandwich",
  "Beef Stroganoff",
  "Grilled Cheese",
  "Blue Cheese Salad",
  "Chicken Wings",
  "Reuben Sandwich",
  "Grilled Cheese",
  "Fish Sandwich",
  "Chicken Pot Pie",
  "Fish Sandwich",
  "Beef Stroganoff"
];

const uniqueDishes = [...new Set(customerDishes)];
console.log(uniqueDishes)
```
