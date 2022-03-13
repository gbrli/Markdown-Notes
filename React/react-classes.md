# Advanced React

## Classes

Basic Class Template. Classes are usually used if lifecycle methods are required on a project.

Props are not passed on like you would to functions: they are automatically passed to classes, and need to be called with `this.props`.

```js
import React from "react"

export default class App extends React.Component {
    render() {
        return (
            <h1>{this.props.type} component</h1>
        )
    }
}
// parent element
ReactDOM.render(<App type="Class" />, document.getElementById("root"))
```

## Class Functions

A function can be declared without using the function keyword inside a class. However, when referencing it in the same class, use the `this` keyword.

```js
toggleGoOut() {...}
// stuff
<div onClick={this.toggleGoOut}>
```

## Class State

State cannot be cast with `useState`. Class components will always save state as a class state that is an object. `setState` is imported from React, so it is always present. An arrow function must be used when setting state.

```js
// state object declaration
state = {
    goOut: "Yes"
}

// calling it
<h1>{this.state.goOut}</h1>

// setting the state object in a toggle function 
toggleGoOut = () => {
    this.setState(prevState => {
        return {
            goOut: prevState.goOut === "Yes" ? "No" : "Yes"
        }
    })
} 
```

## Older Syntax for Class State Declaration

An older way to do this is with a JS constructor method. `super` is imported from React.component. This constructor is used if a codebase does not support JS class fields.

If you can't use arrow functions for class methods, you will have to bind them like in this example.

```js
export default class App extends React.Component {
    constructor() {
        super()
        this.state = {
            goOut: "Yes"
        }
        this.toggleGoOut = this.toggleGoOut.bind(this)
    }
    toggleGoOut() {...}
```

## Lifecycle Methods

Components have a lifecycle of three parts, and each of them includes certain methods:

* Mounting: render(), componentDidMount()
* Updating: render(), componentDidUpdate()
* Unmounting: componentDidUnmount()

`render()` paints elements on the screen, it is called when a component first mounts, and also every time props or state change.

`componentDidMount()` is executed right after render(), but it only runs the first time it is rendered on a page. It is useful for API calls and works similar to useEffect() with an empty dependencies array.

`componentDidUpdate()` runs when props or state change in the component.

```js
// setting state to an object from local storage
state = JSON.parse(localStorage.getItem("formData"))        
// setting the storage to something when components update
componentDidUpdate() {
    localStorage.setItem("formData", JSON.stringify(this.state))
        
    }
```

`componentDidUnmount()` is usually used to remove event listeners, or to remove subscriptions using chat APIs or websockets, so it disconnects once a component is not used anymore.

```js
componentDidMount() {
    window.addEventListener("resize", this.watchWidth)
}    
componentWillUnmount() {
    window.removeEventListener("resize", this.watchWidth)    
}
```

## To try

```js
.then(data => {
    this.setState({character: data})
})

<h1>{this.state.character.name}</h1>
```
