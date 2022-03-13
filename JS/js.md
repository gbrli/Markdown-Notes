# JS

When using numbers as a data type always compare with `===` to be safe.

`textContent` will include white spaces, use it instead of `innerText`.

`querySelector` targets CSS selectors.

`Strings` and `Integers` are primitive data types.

`Arrays` and `Objects` are complex/composite data types.

Variables (especially constants) should be declared at the top of a js program because of hoisting. JS will use a variable even if it hasn't been declared yet. You can also have `use: strict` at the top to avoid this from happening.

`getElementsByClassName` will return an HTML collection of those elements as an array. They can be accessed with `textContent`.

```js
let allNamesDOMCollection = document.getElementsByClassName('name');
console.log(allNamesDOMCollection[1].textContent);
```

## Functions

Function parameters and arguments are the same thing, however:

* they are called parameters when they're inside a function `function add(num1, num)`
* they are called functions when they're invoked from the outside of the function `add(2, 5)`

## Array Notes

```js
let array = [1, 2, 3]
let array = []
```

* push/pop
* shift/unshift

```js
//   START     FINISH   STEP SIZE
for (let i = 1; i < 11; i++)  {    
    console.log(i)
}
```

## Getter

The function below gets the fastest race time with conditional statements by returning the value. All it does is return the needed value. The result is then stored into a separate variable. This essentially makes a variable dynamic.

```js
let player1Time = 102
let player2Time = 107

function getFastestRaceTime() {
    if (player1Time < player2Time) {
        return player1Time
    } else if (player2Time < player1Time) {
        return player2Time
    } else {
        return player1Time
    }
}

let fastestTime = getFastestRaceTime()
```

Dice function example. It is a getter function and it returns a random number like a dice would.

```js
function rollDice() {
    let randomNumber = Math.floor( Math.random() * 6 ) + 1
    return randomNumber
}

console.log( rollDice() )
```

## Objects

They are complex data types with key-value pairs. There are different methods to create objects.
Methods are functions attached to objects. For example in `console.log` the object console uses the method log.

```js
let course = {
    title: "Learn CSS Grid for free",
    lessons: 16,
    creator: "Per Harald Borgen",
    length: 63,
    level: 2,
    isFree: true,
    tags: ["html", "css"]
}
```

Falsey values are the below. Anything else is truthy.

* false
* 0
* ""
* null -> how a developer signalize emptiness
* undefined -> how JavaScript signalizes emptiness
* NaN (not a number)

## Events

The second parameter of an event listener is a function that can take the event itself as a parameter. The `event` object can be used with its own methods within an event listener. The function below return the value of a user input field in lowercase whenever the user releases a key while typing.

```js
document.getElementById('usernameInput').addEventListener('keyup', function(event) {
    let username = event.target.value.toLowerCase();
    console.log(username);
})
```

The function `setinterval(functionName, 1000)` will take any function and repeat it every x milliseconds. The example below will call the function every second. Used in the snake game.

```js
let intervalTime = 1000
let timerId = setInterval(functionName, intervalTime)
clearInterval()
```

`.appendChild` will add an element and return what the element is if you console.log it.

`.append` will not return anything but it will add multiple items at the same time.

## Template Literals

They are a better way to manage strings. They allow to embed expressions within the string in a streamlined way.

```js
const fullName = `${word1} ${word2}`;
```

## Object Destructuring

This is the normal way of getting object values on a player object:

```js
player.name
player.club
```

This is how you can do it with object destructuring:

```js
const { name, club } = player
const { name, projects: {diceGame} } = student
console.log(name, diceGame)
```

## Array Destructuring

Similar to the above. Arrays can be given names to evoke later without an index number.

```js
let [firstName, middleName, lastName] = ['Dylan', 'Clements, 'Israel']
lastName = 'Clements';
console.log(lastName)
```

## Object Literals

They allow to create an object without using a constructor. Example below.

```js
const newAddress = {city: city, state: state}
```

## Example Using Obj Literals and Destructuring

* The function takes a new address parameter.
* The object is destructured into city, state and country, then assigned the parameter of the function.
* The syntax for creating objects is now simplified.
* Invoking the function with the required parameters will create an object.
* This object can only be reached inside the function?

```js
function addressMaker(address) {
    const {city, state, country} = address;
    
    const newAddress = {
        city,
        state,
        country
    };
    console.log(`${newAddress.city}, ${newAddress.state}, ${newAddress.country}`)
}

addressMaker({city: 'Austin', state: 'Texas', country: 'ss'});
```

## For Of Loop

They will iterate an iterable such as arrays or strings, without needing a counter.

```js
let incomes = [62000, 67000, 75000];
let total = 0;

for (const income of incomes) {
    total += income;
}
console.log(total);
```

**The loops below do the same thing!!**

```js
for (let item of array) {
    callback(item)
}

for (let i = 0; i < array.length; i++) {
    callback(array[i])
}
```

## For Each Loop

For Each loops work with arrays. The example below looks inside the numbers array, and logs the index number of each value.

```js
numbers.forEach((number, index) => {
    console.log('Index: ' + index + ' Value: ' + number);
});
```

## Spread Operator and Rest Parameters

A variable declared after an array will reference the array and point to the same place in the computer memory.

```js
let contacts = ["Mary", "Joel", "Danny"]
let personalFriends = contacts
```

The spread operator actually duplicates the original array, and we can also add to it like in the example below.

```js
let contacts = ["Mary", "Joel", "Danny"]
let personalFriends = [ "David", ...contacts, "Lily" ]
```

The same can be done to copy an object.

```js
let employee = {...person}
```

The same syntax is also used for the rest operator. The code below will log the parameters that the function is currently using.

```js
function add(...nums) {
    console.log(nums);
}
add(4, 5, 7, 8, 12)

```

## Arrow Functions

There are three types of function declarations. Regular one:

```js
function breakfastMenu() {
    return "I'm going to scrambled eggs for breakfast";
}
```

Anonymous declaration where a function is not named:

```js
const lunchMenu = function() {
    return "I'm going to eat pizza for lunch";
}
```

Arrow function that will return its content immediately. Note the parameter syntax, one doesn't need brackets, but two or more do:

```js
const dinnerMenu = food => `I'm going to eat a ${food} for dinner`;
const lunchMenu = (food, dessert) => `I'm going to eat ${food} and ${dessert} for lunch`;
console.log( dinnerMenu("chicken salad") );
console.log( lunchMenu("salad", "cake") );
```

These two functions are equivalent:

```js
// ES5
var add = function(x, y) {
  return x + y;
};
// ES6
let add = (x, y) => { return x + y };
```

### Default Parameter in Arrow Functions

When declaring an arrow function, one parameter should be set as a default in case the function is declared without one.

```js
const dinnerMenu = (food = "sandwich") => `I'm going to eat a ${food} for dinner`;
```

## Import/Export

Two JS files can import and export variables, functions, arrays, objects, classes, anything.

```js
export function add(num1, num2) {
    return num1 + num2
}
// on a separate file
import { add } from './data.js'
let adder = add
console.log(adder(1, 8))
```

## Switch Statement

Example below.

```js
    switch(e.keyCode) {
        case 40:
        console.log('pressed down')
        break
        case 38:
        console.log('pressed up')
        break
        case 37: 
        console.log('pressed left')
        break
        case 39:
        console.log('pressed right')
        break
    }
```

## ES6 Classes

A class is a blueprint for creating objects with pre-defined properties and methods. JS is not object-oriented, and this just syntactic sugar. An **instance method** will be available in each instance of the class. A **class method** is instead declared with the `static` keyword, and it will not be accessible from class instance. It will be a utility method exclusive to the actual class only. It can still be called, but by invoking the class itself.

## Class Example

Generates an array of ghosts, and gives them the right class using a forEach loop.

```js
class Ghost {
    constructor(className, startIndex, speed) {
        this.className = className
        this.startIndex = startIndex
        this.speed = speed
    }
}
const ghosts = [
    new Ghost('blinky', 348, 250),
    new Ghost('pinky', 376, 400),
    new Ghost('inky', 351, 300),
    new Ghost('clyde', 379, 500)
]
ghosts.forEach(ghost => squares[ghost.startIndex].classList.add(ghost.className))
```

## Element.children

The code below will grab the first child of the container and place the new content inside it. Whenever an element is selected in JS, it is returned as an HTML collection, and it acts like an array.

```js
document.getElementById("container").children[0].textContent = 'asd'
```

## Pushing a new object with multiple values inside an empty array

```js
const newDice = []
const newNum = {}
for (let i = 0; i < 10; i++) {
    newDice.push({value: Math.ceil(Math.random() * 6), isHeld: false})
}
console.log(newDice)
```

## Get DOM element function

This function will make it easier to get elements by their ID.

```js
const getElement = element => document.getElementById(element)
let nav = getElement("nav");
```

