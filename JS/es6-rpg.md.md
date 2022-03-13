# Next Level JS

`Join()` concatenates array elements into a string and takes a parameter that will be the element separator. `Map()` will return array elements with a comma below, so join is necessary.

```js
const guestList = ['Tom', 'Mary', 'Clare', 'John', 'Liz']

const guestsHtml = guestList.map(function(guest){
	return `<div class="box">${guest}</div>`
	}).join('')

document.getElementById('list').innerHTML = guestsHtml
```

Functions can return another function. This is useful when you need to map over a function that returns an array after applying logic and then you need to render each element individually.

```js
function getDiceRollArray(diceCount) {
	return new Array(diceCount).fill(0).map(() => Math.floor(Math.random() * 6) + 1)

function getDiceHtml(diceCount) {
	return getDiceRollArray(diceCount).map(die => `<div class="dice">${die}</div>`).join("")
}

// down in rendering function
${getDiceHtml(diceCount)}
```

## Array Constructor

These two are equivalent:

```js
const endOfLevelBosses = [undefined, undefined, undefined, undefined, undefined, undefined, undefined, undefined, undefined, undefined]

const endOfLevelBosses = new Array(10)
```

`Fill()` can be used to change every single element to one static value, and map and join can render it all out.

```js
const poisonMushrooms = new Array(100).fill('🍄').map(shroom => `<div class="box">${shroom}</div>`).join('')
```

## Constructors

Functions are objects in JS, so they can have properties indicated with the `this` keyword. Properties on objects that contain functions are called methods.

The keyword `this`  can be used with `Object.assign` to copy the contents of one object to the `this` context of another function. This is possible because functions are objects.

```js
const sandraKayeProfileData = {
	name: 'Sandra Kaye',
	portfolio: 'www.sandrasportfolio.com',
	currentJob: 'Google',
	currentSalary: '400k'	
}

function DevProfile(data){
	Object.assign(this, data)
	this.summariseDev = function(){
    	console.log(`${this.name}'s porfolio is at ${this.portfolio} and they work at ${this.currentJob}. Their current salary is ${this.currentSalary}.`)
    }
}

const sandraKaye = new DevProfile(sandraKayeProfileData)
sandraKaye.summariseDev()
```


## Exports
Exports in modules can be done in two ways: default and named. Default exports are used for single functions. Named exports are used for modules that contain multiple functions.

Default export: `export default characterData` & `import characterData from './data.js'`

Named export: `export {characterData}` & `import {characterData} from './data.js'`


## Reduce

```js
const rainJanuaryByWeek = [ 10, 20, 0, 122 ]

const totalRainfallJanuary = rainJanuaryByWeek.reduce(function(total, currentElement){
    console.log('total: ' + total, 'currentElement: ' + currentElement)
    return total + currentElement
})

console.log(totalRainfallJanuary)
```

## Nested Ternary

```js
const playerGuess = 6
const correctAnswer = 6

const message = playerGuess < correctAnswer ? 'Too low!' 
    : playerGuess > correctAnswer ? 'Too high!' 
    : 'Exactly right!'

console.log(message)
```

## Arrow Function short and long syntax

```js
const speedWarning = speed => `You are going at ${speed} mph!`

const speedWarning = (speedLimit, speed) => {
    if (speed > speedLimit) {
       return `You are going at ${speed} mph!`
    }
}```

## Percentage

`(100 * value) / total value = percentage


## Set Timeout
```js
setTimeout(() => console.log(`Once upon a time, a beautiful princess met a handsome prince.`), 
    2000)

setTimeout(() => console.log(`The princess's wicked stepmother put a curse on them before they could marry.`), 
    4000)

setTimeout(() => console.log(`The prince found a friendly wizard to lift the curse.`), 
    6000)

setTimeout(() => console.log(`They got married on a beautiful summer's day.`), 
    8000)

setTimeout(() => console.log(`In the end, they lived happily ever after.`), 
    10000)
```

## Class

```js
class Module {
    constructor(){
        this.courseName = 'Learn JS'
        this.studentsEnrollded = 5600
        this.studentsCompleted = 5100
    }
}

const learnJs = new Module
```

```js
class Module {
    constructor(data){
        Object.assign(this, data)
        this.percentCompletedModule = this.studentsCompleted / this.studentsEnrolled * 100
    }
    logPercentCompletedModule(){
        console.log(this.percentCompletedModule)
    }
}

const responsiveDesign = new Module(moduleStats.module3)
responsiveDesign.logPercentCompletedModule()
```