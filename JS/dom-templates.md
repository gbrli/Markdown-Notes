# DOM Templates

Function logic goes hand in hand with updating the DOM elements. One change should affect both.

## Basic Onclick Button

Calling the increment() function will keep counting and displaying the number on an HTML element with class `count-el`.

```css
button {
    border: none;
    padding-top: 10px;
    padding-bottom: 10px;
    color: white;
    font-weight: bold;
    width: 200px;
    margin-bottom: 5px;
    border-radius: 5px;
    background: darkred;
}
```

```js
let countEl = document.getElementById("count-el")
let count = 0
function increment() {
    count += 1
    countEl.textContent = count
}
```

## Sorting Array into an HTML ID

```js
let fruit = ["🍎", "🍊", "🍎", "🍎", "🍊"]
let appleShelf = document.getElementById("apple-shelf")
let orangeShelf = document.getElementById("orange-shelf")

function sortFruit() {
    for (let i = 0; i < fruit.length; i++) {
        if (fruit[i] === "🍎") {
            appleShelf.textContent += "🍎"
        } else if (fruit[i] === "🍊") {
            orangeShelf.textContent += "🍊"
        }
    }
}

sortFruit()
```

## Event Listener

First you grab the DOM element, then you add the event listener to it. DOM and code logic move in pairs.

```js
const inputBtn = document.getElementById("input-btn")

inputBtn.addEventListener("click", function() {
    console.log("Button clicked from addEventListener")
})
```

**DO NOT call the function with () on event listeners! Yes to the below, no to handleClick() as a second parameter.**

```js
document.getElementById("new-deck").addEventListener("click", handleClick)
```

## Getting Input Data

The below will push into an array whatever is entered into the HTML input element declared at the top, using the `.value` method.

```js
const inputEl = document.getElementById("input-el")
myLeads.push(inputEl.value)
```

## Adding HTML Elements

Easier way:

```js
let listItems = ""
for (let i = 0; i < myLeads.length; i++) {
    listItems += "<li>" + myLeads[i] + "</li>"
}
ulEl.innerHTML = listItems
```

Alternatively:

```js
const li = document.createElement("li")
li.textContent = myLeads[i]
ulEl.append(li)
```

Template literals can be formatted in any way and this makes them useful for inserting HTML from JS.

```js
```

## Local Storage

You can keep data from a webapp in the browser's local storage using a key/value pair of two strings per the below.

```js
localStorage.setItem("1", "2")
console.log(localStorage.getItem("1"))
localStorage.clear()
```

Parse will turn a string into an array, and stringify will do the opposite. This is used because local storage can only support strings.

```js
let myLeads = []
myLeads.push(inputEl.value)

myLeads = JSON.parse(myLeads)
myLeads = JSON.stringify(myLeads)
```

Check whether a lead is truthy first. If it is, render them in the app.

```js
let leadsFromLocalStorage = JSON.parse( localStorage.getItem("myLeads") )
console.log(leadsFromLocalStorage)

if (leadsFromLocalStorage) {
    myLeads = leadsFromLocalStorage
    renderLeads()
}
```

Array to String:

```js
localStorage.setItem("myLeads", JSON.stringify(myLeads) )
```

String to Array:

```js
let leadsFromLocalStorage = JSON.parse(localStorage.getItem("myLeads"))
```

Retrieve all the contents of the local storage:

```js
JSON.stringify(localStorage);
```

## Interactive Form

* Get entire form and place a **submit** event listener.
* Prevent default behaviour.
* Store the form data in a variable with the object FormData.
* Get the name of the user so you can render it.
* Generate an acknowledgement of receipt message and store it in a variable
* Get the main content of the page where the form was and fill it with the generated text instead.

```js
let emailCollectorForm = document.getElementById("Email-Collector")
emailCollectorForm.addEventListener("submit", event => {
    event.preventDefault()    
    let ourFormData = new FormData(event.target)    
    let userFirstName = ourFormData.get("firstName")    
    let updatedHtmlContent = `
        <h2>Congratulations, ${userFirstName}!</h2>

        <p>You're on your way to becoming a BBQ Master!</p>
        
        <p class="fine-print">We'll never share your information without your permission</p>
    `
    let ourMainContent = document.getElementById("Main-Content")
    ourMainContent.innerHTML = updatedHtmlContent
})
```

## Clock

The function below will get the current date, format the local time, and with `setInterval()` it will call it every second to update the value on the DOM.

```js
function getCurrentTime() {
    const date = new Date()
    document.getElementById("time").textContent = date.toLocaleTimeString("en-us", {timeStyle: "short"})
}

setInterval(getCurrentTime, 1000)
```

## Rolling function that checks for decimal points. Don't forget toFixed() when calling it

```js
function roll(min, max, floatFlag) {
    let r = Math.random() * (max - min) + min
    return floatFlag ? r : Math.floor(r)
}
```
