# Context

Until now the only way to pass data to a component's sibling was to move state to a higher component and then pass it back down to the sibling via props. This process is known as prop drilling and it's both tedious and time-consuming.

This is where Context comes in. It uses a **Provider**, which is a common parent of the elements which need the data and a **Consumer**, which is wrapped around the components which need the data.

React passes data through the component tree via the Provider-Consumer pair without having to pass props down through every level.

* Only use context if you have more than two layers. Otherwise, prop drilling is fine. Use better composition first.
* Do not use context for state that should be kept locally, such as forms.
* Don't make the initial App the Provider. Use the closest parent to all Consumers.
* If passing objects as values, performance can be an issue.

## Class Component with Static Context

Context provider component:

```js
import React from "react"
const ThemeContext = React.createContext()
export default ThemeContext
```

index.js:

```js
import ThemeContext from "./themeContext"
// passing a required value to toggle light/dark theme
ReactDOM.render(
    <ThemeContext.Provider value={"dark"}>
        <App />
    </ThemeContext.Provider>, 
    document.getElementById("root")
)
```

Button class component:

```js
import React, {Component} from "react"
import ThemeContext from "./themeContext"
// 
class Button extends Component {
    render() {
        const theme = this.context
        return (
            <button className={`${theme}-theme`}>Switch Theme</button>
        )    
    }
}
// the below will add a static property
Button.contextType = ThemeContext
export default Button
```

## Functional Component

All you have to do is create the context component and specify the provider in index.js like above, then use a function to call the props children (similar to render props) and wrap it in a consumer.

```js
function Button(props) {
    return (
        <ThemeContext.Consumer>
            {theme => (
                <button className={`${theme}-theme`}>Switch Theme</button>
            )}
        </ThemeContext.Consumer>
    )    
}
```

Context provider in its own component:

```js
// context component
import React, {Component} from "react"
const {Provider, Consumer} = React.createContext()

class ThemeContextProvider extends Component {
    render() {
        return (
            <Provider value={"dark"}>
                {this.props.children}
            </Provider>
        )
    }
}
export {ThemeContextProvider, Consumer as ThemeContextConsumer}

// importing context on other components
import {ThemeContextConsumer} from "./themeContext"
/.../
<ThemeContextConsumer>...<ThemeContextConsumer>
//
```
