# React

React is composable, meaning you can build one component at a time and reuse them indefinitely.

It is also declarative rather than imperative. This means that you are telling the program what you want to build and the program will know what to do. In imperative programming, such as vanilla JS, you tell the machine exactly what the steps are to build something.

JSX is Javascript XML. The content placed in the first argument of `render()` is in JSX, and it is used by React to generate a JS object that describes the DOM element we're going to place on the page.

A React component is a React function that returns Reach elements to modify the DOM with JSX. They are named with Pascal Case and are called with `<Name />`.

Styling is done by giving elements classes. In JSX, you can do it by adding `className="asd"`.

React's primary tasks are rendering the UI by working with the DOM, managing state so values can be remembered between render cycles, and keeping the UI updated when those state changes occur.

## Basic React DOM Render

```js
function NavBar() {
    return (
        <nav>
            <h1>Bob's Bistro</h1>
            <ul>
                <li>Menu</li>
                <li>About</li>
                <li>Contact</li>
            </ul>
        </nav>
    )
}
ReactDOM.render(<NavBar />, document.getElementById("root"))
```

## Easy Setup for Practice

```html
<html>
    <head>
        <link rel="stylesheet" href="index.css">
        <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
        <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
        <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
    </head>
    <body>
        <div id="root"></div>
        <script src="index.js" type="text/babel"></script>
    </body>
</html>
```

## Proper Setup

Add dependencies in local envinronment. Remember to import the dependencies.

```js
import React from "react"
import ReactDOM from "react-dom"
```

## Self Closing HTML Tags

Self closing tags such as `<img>` must be closed in JSX. `<img src="x.jpg"/>`

## Parent/Child

Functions to generate components can be called within another function. The below common practice.

```js
function Page() {
    return (
        <div>
            <Header />
            <MainContent />
            <Footer />
        </div>
    )
}
```

## Importing Files

Components should be stored in different pages to keep them separate.

```js
import Footer from "./Footer"
```

```js
import React from "react"

export default function Footer() {
    return (
        <footer>
            <small>© 2021 Ziroll development. All rights reserved.</small>
        </footer>
    )
}
```

## Default Props

Default props provide a default value to use in case a value is missing or something goes wrong.

```js
function Card(props) {
    const styles = {
        backgroundColor: props.cardColor,
        height: props.height,
        width: props.width
    }
    
    return (
        <div style={styles}></div>
    )
}
// default will always be blue and 100x100
Card.defaultProps = {
    cardColor: "blue",
    height: 100,
    width: 100
}
// rendering in App with different values
<Card cardColor="red" height={200} width={400} />
```

## Prop Types

Prop types can be used during development to ensure that a prop is coming through with the right type.

```js
import PropTypes from "prop-types"

Card.propTypes = {
    cardColor: PropTypes.oneOf(["red", "blue", "green", "purple"]).isRequired,
    height: PropTypes.number.isRequired,
    width: PropTypes.number
}
```

## Create Project with My React App

Ideally use Webpack and Babel instead. However My React App is enough to start.

The code below will create a project in a folder.

```terminal
npx create-react-app my-app
cd my-app
npm start
```

## Font Awesome Setup

```js
npm i --save @fortawesome/fontawesome-svg-core
npm install --save @fortawesome/free-solid-svg-icons
npm install --save @fortawesome/react-fontawesome
npm install --save @fortawesome/free-brands-svg-icons
npm install --save @fortawesome/free-regular-svg-icons
```

## Fix images and style in Create React App

* Keep style.css in the src folder with index.js and `import "./style.css"`
* Put images in their own folder and `import logo from "../images/logo.png"`
* Then, reference it with `<img src={logo} />` instead of hardcoding it directly here.
* For using map() with images, have The images directory inside the public directory

## Props as Parameters

Props are used to make components reusable. They are used like function parameters, and they are always objects when received by a component. Objects can also be destructured, but it's not as tidy. The examples below do the same thing.

Props are properties being passed to a component so it can function properly. The component is not allowed to modify the props, which are immutable.

```js
// prop on a parent
<Header username="bobziroll" />
// prop on a child
<p>Welcome, {props.username}!</p>
```

**Objects should be interacted with on the component page, not on the general App.js.**

```js
export default function Contact(props) {
    return (
        <div className="contact-card">
            <img src={props.img}/>
            <h3>{props.name}</h3>
        </div>
    )
}
export default function Contact({img, name}) {
    return (
        <div className="contact-card">
            <img src={img}/>
            <h3>{name}</h3>
        </div>
    )
}
```

The `App.js` file should instead be calling the imported function from above, with the prop values. Everything is strings, unless it's in {} to specify numbers.

```js
function App() {
    return (
        <Contact 
            img="./images/mr-whiskerson.png" 
            name="Mr. Whiskerson"
            phone={(212) 555-1234}
            email="mr.whiskaz@catnap.meow"
        />
```

## Array Methods (Map)

Arrays methods can be used to render arrays with React. The code below loops over an array with two parameters and returns each of them using Map. The value returned from the function is stored in a variable, and that is returned in the `div` element for the DOM.

Map is very commonly used to convert raw data into an array of JSX elements to render.

```js
export default function App() {
    const jokeElements = jokesData.map(joke => {
        return <Joke setup={joke.setup} punchline={joke.punchline} />
    })
    return (
        <div>
            {jokeElements}
        </div>
    )
}
```

```js
import React from "react"
import Navbar from "./components/Navbar"
import Hero from "./components/Hero"
import Card from "./components/Card"
import data from "./data"

export default function App() {
    const cards = data.map(item => {
        return (
            <Card 
                key={item.id}
                img={item.coverImg}
                rating={item.stats.rating}
                reviewCount={item.stats.reviewCount}
                location={item.location}
                title={item.title}
                price={item.price}
            />
        )
    })        
    
    return (
        <div>
            <Navbar />
            {cards}
        </div>
    )
}
```

**Rather than doing all of the above, return the entire item like such:**

```js
export default function App() {
    const cards = data.map(item => {
        return (
            <Card
                key={item.id}
                item={item}
            />
        )
    })        
    return (
        <div>
            <Navbar />
            <section className="cards-list">
                {cards}
            </section>
        </div>
    )
}

// meanwhile Card should have:

export default function Card(props) {
    return (
        <div className="card">
            <img src={`../images/${props.item.coverImg}`} className="card--image" />
            <span>{props.item.stats.rating}</span>
```

## Check a value to create a custom property

```js
let badgeText
if (props.openSpots === 0) {
    badgeText = "SOLD OUT"
} else if (props.location === "Online") {
    badgeText = "ONLINE"
}
// place below inside rendering parent
{badgeText && <div className="card--badge">{badgeText}</div>}
```

## Hooks: State and Effect

useState returns an array of two elements: the first element is the actual state, and the second is a function. You are expected to destructure it.

```js
function App() {
    const [count, setCount] = useState(0)
    
    function increment() {
        setCount(prevCount => prevCount + 1)
    }
    
    function decrement() {
        setCount(prevCount => prevCount - 1)
    }
    
    return (
        <div>
            <h1>{count}</h1>
            <button onClick={increment}>Increment</button>
            <button onClick={decrement}>Decrement</button>
        </div>
    )
}
```

useEffect with a working setInterval

```js
import React, {useState, useEffect} from "react"
import randomcolor from "randomcolor"

function App() {
    const [count, setCount] = useState(0)
    const [color, setColor] = useState("")
    
    useEffect(() => {
        const intervalId = setInterval(() => {
        }, 1000)
        return () => clearInterval(intervalId)
    }, [])
    
    useEffect(() => {
        setColor(randomcolor())
    }, [count])
    
    function increment() {
        setCount(prevCount => prevCount + 1)
    }
    
    function decrement() {
        setCount(prevCount => prevCount - 1)
    }
    
    return (
        <div>
            <h1 style={{color: color}}>{count}</h1>
            <button onClick={increment}>Increment</button>
            <button onClick={decrement}>Decrement</button>
        </div>
    )
}

export default App

```

## State vs Props

Props pass data to a component, and then the component determines what to display on a page.

State referes to the values that are managed by a component, the same way variables are used in a function. State is used to maintain values defined within the component when rendering the page.

## Create State variable

```js
const [isShown, setIsShown] = React.useState(false)
```

## Simple Toggle Function

```js
function toggle() {
        console.log(isShown)
        setIsShown(!isShown) 
// alternative: setIsShown(prevShown => !prevShown)
    }
```

## Add Onclick event in JSX

```js
<button onClick={toggle}>Toggle</button>
```

## Passing Parameters with a Function on an event

```js
onClick={(event) => props.deleteNote(event, note.id)}
```

## Declaring and Changing State Variables

When declaring a variable, use `React.useState()` to ensure the state will be used. `useState()` returns an array of two items, the variable and a function. The code below uses array destructuring to avoid having to type `count[0]` when rendering.

If you need to modify the state variable, **do not** change it directly with `count = 1` or `count++`. You need to reference the old value instead and update it in a callback function, like the arrow function below. You can also change it directly with `setCount(3)`.

```js
// state (variable) declaration
    const [count, setCount] = React.useState(0)
    function add() {
        setCount(prevCount => prevCount + 1)
    }
// rendering below
    <h1>{count}</h1>
```

Using a boolean and a ternary operator for a toggle yes/no button:

```js
let [isGoingOut, setIsGoingOut] = React.useState(true);
function changeValue() {
    setIsGoingOut(!isGoingOut)
} 
return (
    <div className="state">
        <h1 className="state--title">Do I feel like going out tonight?</h1>
        <div className="state--value" onClick={changeValue}>
            <h1>{isGoingOut ? "Yes" : "No"}</h1>
```

One more complete example:

```js
import React from 'react';
import ReactDOM from 'react-dom';

function App() {
    const [thingsArray, setThingsArray] = React.useState(["Thing 1", "Thing 2"])
    
    function addItem() {
        setThingsArray(prevState => {
            return [...prevState, `Thing ${prevState.length + 1}`]
        })
    }
    
    const thingsElements = thingsArray.map(thing => <p key={thing}>{thing}</p>)
    
    return (
        <div>
            <button onClick={addItem}>Add Item</button>
            {thingsElements}
        </div>
    )
}

ReactDOM.render(<App />, document.getElementById('root'));
```

## Modifying an Object

The entire object needs to be recreated with a spread operator. The property we want to change then needs to be overwritten like the boolean value below.

```js
    const [contact, setContact] = React.useState({
        firstName: "John",
        lastName: "Doe",
        phone: "+1 (719) 555-1212",
        email: "itsmyrealname@example.com",
        isFavorite: false
    })
// Arrow function    
    function toggleFavorite() {
        setContact(prevContact => ({
            ...prevContact,
            isFavorite: !prevContact.isFavorite
        }))
    }
// Regular function with return
        function toggleFavorite() {
        setContact(prevContact => {
            return {
                ...prevContact,
                isFavorite: !prevContact.isFavorite
            }
        })
    }
```

## Passing a state as props

A child component can receive a state value via props.

```js
// passing states as props when invoking the child
<Count number={count} />
// declaring the child
export default function Count(props) {
    return (
            <h1>{props.number}</h1>
    )
}
```

## Setting a parent state from a child component

States and functions can be passed from a parent to a child, and the child can modify them using props.

```js
// parent
function toggleFavorite() {
    setContact(prevContact => ({
        ...prevContact,
        isFavorite: !prevContact.isFavorite
    }))
}

<Star isFilled={contact.isFavorite} handleClick={toggleFavorite} />

//child
export default function Star(props) {
    const starIcon = props.isFilled ? "star-filled.png" : "star-empty.png"
    return (
        <img 
            src={`../images/${starIcon}`} 
            onClick={props.handleClick}
        />
    )
}
```

Parent can pass data to children, but sibling elements do not communicate with each other. There are third party solutions to help with moving data between elements such as Redux.

Simple example of moving data around with props:

```js
// parent
import React from "react"
import Header from "./Header"
import Body from "./Body"

export default function App() {
    const [user, setUser] = React.useState("Joe")
    return (
        <main>
            <Header x={user} />
            <Body x={user} />
        </main>
    )
}

// child
import React from "react"
export default function Header(props) {
    return (
        <header>
            <p>Current user: {props.x}</p>
        </header>
    )
}
```

## Setting Styles from React

Styles can be setup within a component. Using a ternary operator with a predetermined property of darkmode can be used to trigger themes on a page.

```js
export default function Box(props) {
    const styles = {
        backgroundColor: props.on ? "#222222" : "transparent"
    }
    return (
        <div 
            style={styles} 
            className="box"
            onClick={props.toggle}
        >
        </div>
    )
}
```

## Conditional Rendering

The AND operator `&&` works by first checking whether the first condition is truthy, than running the second and checking whether that's truthy as well.

This can be used in React to render code that fulfills one condition (on the left), and it's called **conditional rendering**.

```js
{isShown && <p>{props.punchline}</p>}
```

Using conditional rendering with a ternary operator.

```js
messages.length === 0 ?
<h1>You're all caught up!</h1> :
<h1>You have {messages.length} unread {messages.length > 1 ? "messages" : "message"}</h1>
```

## Forms in React

Forms are not as straigtforward in React. An event should be used to pass what is happening in the form, and the below sets the state variable to the value of the target of the event, meaning, what is being inputted in the form when the state changes.

```js
const [firstName, setFirstName] = React.useState("")
function handleFirstNameChange(event) {
        setFirstName(event.target.value)
            //
            <input
                type="text"
                placeholder="First Name"
                onChange={handleFirstNameChange}
            />        
```

## Multiple Inputs on a Form

Multiple inputs require a state object, not just one state variable. Inputs should have the same name of their object keys.

When updating the state, the previous form data must be called, placed in a new object, and the property we need must be overwritten. `[event.target.name]: event.target.value` does that.

```js
export default function Form() {
    const [formData, setFormData] = React.useState(
        {firstName: "", lastName: ""}
    )
        
    function handleChange(event) {
        setFormData(prevFormData => {
            return {
                ...prevFormData,
                [event.target.name]: event.target.value
            }
        })
    }
     
    return (
        <form>
            <input
                type="text"
                placeholder="First Name"
                onChange={handleChange}
                name="firstName"
                value={formData.firstName}
            />
            <input
                type="text"
                placeholder="Last Name"
                onChange={handleChange}
                name="lastName"
                value={formData.lastName}
            />
        </form>
    )
}

```

## Controlled Components

The inputs in the example above are controlled by the addition of `value={formData.lastName}`. Without that, the form element will control the state. By adding that line, the value will be controlled by the state directly as it should be. There should only be one source of truth from the parent element so do include that line on each form element.

## Form Elements Best Practice

Regular inputs, checkboxes, radio buttons, select from menu, and submit button.

All buttons inside a form in react are considered submit buttons, so you don't need `type="submit"`. The `handleSubmit` function is defined in the form tag.

```js
import React from "react"

export default function Form() {
    const [formData, setFormData] = React.useState(
        {
            firstName: "", 
            lastName: "", 
            email: "", 
            comments: "", 
            isFriendly: true,
            employment: "",
            favColor: ""
        }
    )
    
    function handleChange(event) {
// destructuring the event object takes the values from the JSX element
        const {name, value, type, checked} = event.target
        setFormData(prevFormData => {
            return {
                ...prevFormData,
                [name]: type === "checkbox" ? checked : value
            }
        })
    }
    
    function handleSubmit(event) {
        event.preventDefault()
        // submitToApi(formData)
        console.log(formData)
    }
    
    return (
        <form onSubmit={handleSubmit}>
            <input
                type="text"
                placeholder="First Name"
                onChange={handleChange}
                name="firstName"
                value={formData.firstName}
            />
            <input
                type="text"
                placeholder="Last Name"
                onChange={handleChange}
                name="lastName"
                value={formData.lastName}
            />
            <input
                type="email"
                placeholder="Email"
                onChange={handleChange}
                name="email"
                value={formData.email}
            />
            <textarea 
                value={formData.comments}
                placeholder="Comments"
                onChange={handleChange}
                name="comments"
            />
            <input 
                type="checkbox" 
                id="isFriendly" 
                checked={formData.isFriendly}
                onChange={handleChange}
                name="isFriendly"
            />
            <label htmlFor="isFriendly">Are you friendly?</label>
            <br />
            <br />
            
            <fieldset>
                <legend>Current employment status</legend>
                <input 
                    type="radio"
                    id="unemployed"
                    name="employment"
                    value="unemployed"
                    checked={formData.employment === "unemployed"}
                    onChange={handleChange}
                />
                <label htmlFor="unemployed">Unemployed</label>
                <br />
                
                <input 
                    type="radio"
                    id="part-time"
                    name="employment"
                    value="part-time"
                    checked={formData.employment === "part-time"}
                    onChange={handleChange}
                />
                <label htmlFor="part-time">Part-time</label>
                <br />
                
                <input 
                    type="radio"
                    id="full-time"
                    name="employment"
                    value="full-time"
                    checked={formData.employment === "full-time"}
                    onChange={handleChange}
                />
                <label htmlFor="full-time">Full-time</label>
                <br />
            </fieldset>
            <br />
            
            <label htmlFor="favColor">What is your favorite color?</label>
            <br />
            <select 
                id="favColor" 
                value={formData.favColor}
                onChange={handleChange}
                name="favColor"
            >
                <option value="red">Red</option>
                <option value="orange">Orange</option>
                <option value="yellow">Yellow</option>
                <option value="green">Green</option>
                <option value="blue">Blue</option>
                <option value="indigo">Indigo</option>
                <option value="violet">Violet</option>
            </select>
            <br />
            <br />
            <button>Submit</button>
        </form>
    )
}
```

## Effect Hook

React can't handle anything outside its reach, such as APIs or local storage. A fetch call to an API that updates a state variable will cause the page to render again upon the state change, and that will fetch from the API again, in a constant loop.

`useEffect()` allows certain code to be executed according to the values in the dependencies array. If those values stay the same, `useEffect` will not run. If the values in the array change, it will.

`useEffect()` must be used with a callback function, ideally an arrow.

```js
    React.useEffect(() => {
        console.log("Effect function ran")
    }, [count])
```

If the dependencies array is empty, the code will only be executed on the first page render.

```js
React.useEffect(function() {
    fetch("https://swapi.dev/api/people/1")
        .then(res => res.json())
        .then(data => setStarWarsData(data))
}, [])
```

## Cleanup Function in Use Effect

Use effect takes two parameters, a function and the dependencies array. However, the first function takes up a return function itself. This can be used like below to clean up and remove the event listener.

```js
React.useEffect(() => {
    function watchWidth() {
        console.log("Setting up...")
        setWindowWidth(window.innerWidth)
    }
    
    window.addEventListener("resize", watchWidth)
    
    return function() {
        console.log("Cleaning up...")
        window.removeEventListener("resize", watchWidth)
    }
}, [])
```

## Lazy State Initialization

When declaring a state, keep in mind that every time the state is updated somewhere else in the code, everything gets rendered again. A solution to this is lazy state initialisation: instead of providing useState with a value, provide it with a function that returns a value, and it won't run when rendered.

```js
// this will rener again
const [notes, setNotes] = React.useState(
    JSON.parse(localStorage.getItem("notes")) || []
)
// arrow function prevents rendering again
const [notes, setNotes] = React.useState(
    () => JSON.parse(localStorage.getItem("notes")) || []
)
```

## Passing Parameters to component

Note the arrow function calling a separate function with a parameter.

```js
const diceElements = dice.map(die => (
    <Die key={die.id} value={die.value} isHeld={die.isHeld} holdDice={() => holdDice(die.id)} />
))
```

## Changing one object parameter inside an array of objects

This function needs to update an object property inside an array in a state variable. First we call setDice, then we get the old array because only one property needs to change and we need to keep the rest of the old array. Then we map the old array, and only return the property we need if it is identical to the holdDice function parameter. If it is, we return the entire single die array with only one property changed. Otherwise we return die as it is.

```js
function holdDice(id) {
    setDice(oldDice => oldDice.map(die => {
        return die.id === id ? 
            {...die, isHeld: !die.isHeld} :
            die
    }))
}
```
