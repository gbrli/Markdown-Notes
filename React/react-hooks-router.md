# Hooks and Router

## Hooks

Hooks are functions that let you “hook into” React state and lifecycle features from function components. They let you use React without classes. Hooks are used to retain values during the entire lifespan of a component.

The `useRef()` hook can be used to grab a DOM node on the screen instead of `getElementById`, and usually it is given the null parameter since it will be changed.

```js
const inputRef = React.useRef(null)
// inputRef is an object that contains a current property. Adding focus() will keep the focus in the input field after running this line in a function
inputRef.current.focus()
// ref will set the input box to inputRef
<input ref={inputRef} type="text" name="todo" value={newTodoValue} onChange={handleChange}/>
```

The `useContext()` hook replaces context provider and consumers. It takes as a parameter the previous provider component.

```js
// placed on consumer component
const context = useContext(ThemeContext)
return (
    <h2>{context.theme === "light" ? "Light" : "Dark"} Theme</h2>    
)

// entire context provider
import React, {useState} from "react"
const ThemeContext = React.createContext()

function ThemeContextProvider(props) {
    const [theme, setTheme] = useState("dark")
    
    function toggleTheme() {
        setTheme(prevTheme => prevTheme === "light" ? "dark" : "light")
    }
    // the const declared above has a .Provider property
    return (
        <ThemeContext.Provider value={{theme, toggleTheme}}>
            {props.children}
        </ThemeContext.Provider>
    )
}

export {ThemeContextProvider, ThemeContext}

```

## Custom Hooks

Reusability patterns can be improved with custom hooks. Since hooks are just functions anyway, you can easily create one and import it on any componenet.

Destructuring the object forces you to keep the same name across components because count and increment in the example below are actually keys to the object: `count: count` and `increment: increment`. Alternatively, a more flexible solution is to return and invoke an array by simply changing the brackets below. This will enable using different names across components.

```js
// custom hook with counter function
import {useState} from "react"

function useCounter() {
    const [count, setCount] = useState(0)
    
    function increment() {
        setCount(prevCount => prevCount + 1)
    }
// returns an object with state and function    
    return {count, increment}
}

export default useCounter

// invoking it while also destructuring the object
import useCounter from "./useCounter"

function App() {
    const {count, increment} = useCounter()
    ...
}
```

## React Router

React Router is a way to create single-page-applications (SPAs), meaning websites with multiple pages. Normally, a website would have multiple pages that need to be requested and sent back from a server. With a SPA, conditional rendering is used in React to render only the parts that need to change.

Browser Router below is a context provider that we use to wrap the main App in.

Importing `{Link}` enables multiple pages: `<Link to>` replaces `<a href>` tags.

`{Route}` provides routes to render so components can be loaded.

`{Switch}` determines which of the routes provided should be rendered.

Nested routes should be specified within `Switch` inside the component they need to be rendered. Simply add the full directory on the path and use `exact path` if the shared name causes issues.

```js
import React from "react"
import ReactDOM from "react-dom"
import {BrowserRouter as Router} from "react-router-dom"
import App from "./App"

ReactDOM.render(
    <Router>
        <App />
    </Router>, 
    document.getElementById("root")
)
```

Navbar setup example using Link, Switch and Router:

```js
import React from "react"
import {Switch, Route, Link} from "react-router-dom"
import Home from "./Home"
import About from "./About"
import Contact from "./Contact"

function App() {    
    return (
        <div>
            <nav>
                <Link to="/">Home</Link>
                <Link to="/about">About</Link>
                <Link to="/contact">Contact</Link>
            </nav>
            
            <Switch>
                <Route exact path="/">
                    <Home/>
                </Route>
                <Route path="/about">
                    <About/>
                </Route>
                <Route path="/contact">
                    <Contact/>
                </Route>
            </Switch>
        </div>
    )
}

export default App
```

## Passing Props in Router

The easiest way to pass props in Router is to use custom hooks provided by router-dom.

```js
import {useLocation, useParams, useHistory, useRouteMatch} from "react-router-dom"
```

When declaring a route, Router accepts route variables declared with colons. The custom hook `useParams()` is used here.

A variable inside of a Route is known as a route param and allows us to have one Route which handles any nested routes down the line.

```js
<Route path="/services/:serviceId" >
    <ServiceDetail />
</Route>

// object destructured to avoid writing something.serviceId
import {useParams} from "react-router-dom"
    const {serviceId} = useParams()
// finding all arrays where the id on the path matches the id on an external json data file
    const thisService = servicesData.find(service => service._id === serviceId)
// rendering each value in the objects
    return (
        <div>
            <h1>Service Detail Page</h1>
            <h3>{thisService.name} - ${thisService.price}</h3>
            <p>{thisService.description}</p>
        </div>
    )
}
```

```js
// mapping all objects inside one array and rendering name and price keys inside each object:
const services = servicesData.map(service => (
        <h3>{service.name} - ${service.price}</h3>
    ))
    return (
        <div>
            <h1>Services List Page</h1>
            {services}
        </div>
    )
```

`useRouteMatch()` allows us to match a path with a url and create a route dynamically.

```js
const { path, url } = useRouteMatch()
    <Link to={`${url}/info`}>Profile Info</Link>
    <Route path={`${path}/info`}>
```

`useHistory()` is used when certain code needs to run before redirecting a user. It allows us to move back and forth in the history of an application. If you're just moving between links on a website though, just use `<Link>`. It has its own methods and they are visible by console logging useHistory.

```js
const history = useHistory()
function handleClick() {
    console.log("Submitting...")
    setTimeout(() => {
        history.goBack()
    }, 2000)
}
```

`useLocation()` gives access to the path you are currently at inside the app.

```js
const location = useLocation()
```

`<Redirect>` is usually implemented with authentication pages. `<Link>` and `<History>` should be used if you need to move across pages first. The below will have a state to check before redirecting a user to a login page.

```js
const [isLoggedIn, setIsLoggedIn] = useState(false)
    <Route path="/private">
        {
            isLoggedIn ?
            <h1>Protected page, must be logged in to be here</h1> :
            <Redirect to="/login" />
        }
    </Route>
```
