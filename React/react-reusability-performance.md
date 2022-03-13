# Reusability and Performance

The best ways to keep code DRY are usually inheritance, like in OOP, and composition. The React dev team recommend using composition rather than inheritance.

**Inheritance is based on what a component IS (cat -> animal).
Composition is based on what a component DOES (eats -> purrs).**

* Create components with props
* Children
* Higher-order components (replaced by hooks)
* Render props (replaced by hooks)

## Children

Children can be passed to components like props. However, the best option is still to have a component with `<img>` and `<p>`, and then pass the image and text as props.

```js
// app
<CTA>
    <h1>This is an important CTA</h1>
    <button>Click me now or you'll miss out!</button>
</CTA>
// component
<div className="border">
{props.children}
</div>
```

## Higher Order Components

A HO function is a function that takes another function as a parameter, like .map().

A HO component is a function that takes a componenet as a parameter and returns a new component. The resulting component is the old one wrapped by the function and with extra capabilities.

The function below takes an empty component, and returns a function using props that will return the new Basic component with the property number and all of the previous props. It needs to be imported in the App componenent, and also exported from it.

HOC can be used to avoid duplicated logic in multiple components, for example toggle functions. It is more common to use hooks, but legacy code will have HOCs.

```js
// parent export should be at the bottom
import {withFavoriteNumber} from "./withFavoriteNumber"
...
export default withFavoriteNumber(App)

// component
export function withFavoriteNumber(comp) {
    const Basic = comp
    return function(props) {
        return (
            <Basic number="4" {...props} />
        )        
    }
}
```

## Render Props

They get the name simply from rendering props that are sent to components, usually as function parameters. Props can pass any data type or a function to components. They are simpler to use than HOCs.

```js
// this will pass an array to the example component
<Example name={["Bob", "Joe"]}
// this will pass a function - parent
<Example name={function() {return "Hey there"}} />
/* component */ 
return <h1>Hi {props.name()}</h1>
```

This prop function will pass on a parameter.

```js
<Example render={
    function(name) {
        return <h1>Hey there, {name}</h1>
    }
{props.render("Sarah")}
```

Passing an object containing an array and returning each part as an h1 element:

```js
<Example render={
    function() {
        let arr = {key: 1, y: [1,2,3,4,5,6,7]}
        return arr.y.map(x => <h1>{x}</h1>
        )
    }
}/>
```

One useful way to use this is having a toggler component that is reused throughout the project like below.

```js
class Toggler extends Component {
    // state set on default with a default props below
    state = {
        on: this.props.defaultOnValue
    }
    static defaultProps = {
        defaultOnValue: false
    }
    // toggle function to change state above
    toggle = () => {
        this.setState(prevState => ({on: !prevState.on}))
    }
    // component returns a destructured object with the state and the toggle function to change it
    render() {
        return (
            <div>
                {this.props.render({
                    on: this.state.on, 
                    toggle: this.toggle
                })}
            </div>
        )
    }
}

export default Toggler
```

```js
import Toggler from "./Toggler"
function Menu(props) {
    return (
    // Toggler component is invoked and a function called render() is taking two parameters (a destructured object of what is in the toggler above)
    // toggle and on from the function are being used to display the menu below
        <Toggler defaultOnValue={true} render={({on, toggle}) => (
            <div>
                <button onClick={toggle}>{on ? "Hide" : "Show"} Menu </button>
                <nav style={{display: on ? "block" : "none"}}>
                    <p><a>Your Profile</a></p>
                </nav>
            </div>
        )}/>
    ) 
}
```

The above can also be achieved using children.

```js
// toggler comp
render() {
    return (
        <div>
            {this.props.children({
                on: this.state.on, 
                toggle: this.toggle
            })}
        </div>
    )
}
// parent
<Toggler defaultOnValue={true}>
    {({on, toggle}) => {
        return (
        <Menu on={on} toggle={toggle}/>
    )}}
</Toggler>
```

## Tree Rendering and Performance

React renders components recursively down one branch until there are no more to render. A grandparent comp will render a parent comp and then its child and its grandchild, then move on to the next parent, child and grandchild, etc.

Changes to state and props will recursively re-render down the remaining tree, whether those components have changed or not. This is a problem if state is being held in the App component, and there are three tools to avoid this.

`shouldComponentUpdate()` allows to determine if a component should update or not. It takes the upcoming props and state as parameters. It must return true or false but there is no need to use this.

`React.PureComponent` is an import, and it implements shouldComponentUpdate() automatically. Extend it on parents and children alike. However, this only works on class components

```js
React, {PureComponent} from "react"
class GrandParent extends PureComponent
```

`React.memo()` was made to be used with functional components instead. It only compares prevPros and nextProps, not state. It takes a componenet and optimizes through memoization.

```js
function Parent(props) {...}
export default React.memo(Parent)
```
