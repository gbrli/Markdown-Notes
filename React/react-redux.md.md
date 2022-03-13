# Redux

Redux was created to manage global app state before React's context API was stable enough to use.

* One single source of truth in a global state
* State is read-only, and components can emit actions that Redux uses to update state
* Changes are made with pure functions called reducers

```js
// importing redux in JS without React
const redux = require("redux")

// creating a store that takes a reducer function as a parameter
const store = redux.createStore(reducer)
```

The fundamental parts of the Redux library are:

* Actions and action creators
* Dispatch
* Reducers
* Store

## Actions and action creators

Actions are objects with a `type` property. The value of type is a string that describes the action you want to make.

An action creator is a function that returns an action object.

```js
// action
const action = {
	type: "INCREMENT"
}

// action creator
function increment() {
    return {
        type: "INCREMENT"
    }
}
```

## Reducer

A reducer takes the old state and an action, and returns a new state based on the incoming action type. Switch statements are perfect for the job but if statements can be used too.

```js
function reducer(state = {count: 0}, action) {
    switch(action.type) {
        case "INCREMENT":
            return {
                count: state.count + 1
            }
        case "DECREMENT":
            return {
                count: state.count - 1
            }
        default:
            return state
    }
}
```

## Store

A store must be created to get access to `subscribe()`, `dispatch()` and `getState()`.

Subscribe() will perform the operations in its function body after a state change occurs in the store.

GetState() will quickly get the current state of the app.

Dispatch() will take an action and send it to the reducer function.

```js
const store = redux.createStore(reducer)

store.subscribe(() => {
    console.log(store.getState())
})
// function returning an object and hardcoded object value, are equivalent
store.dispatch(increment())
store.dispatch({type: "INCREMENT"})
```

## Payload

An action can also return an object with a payload value that is a parameter passed to it.

```js
const redux = require("redux")

function changeCount(amount) {
    return {
        type: "CHANGE_COUNT",
        payload: amount
    }
}

function reducer(state = {count: 0}, action) {
    switch(action.type) {
        case "CHANGE_COUNT":
            return {
                count: state.count + action.payload
            }
        default:
            return state
    }
}

const store = redux.createStore(reducer)
store.subscribe(() => {
    console.log(store.getState())
})

store.dispatch(changeCount(5))
```

## More complex state

When updating more than one state at a time, the previous state must be returned or it will be overwritten completely by the new one. This is done as usual with the `...` operator.

```js
const initialState = {
    count: 0,
    favoriteThings: []
}

function reducer(state = initialState, action) {
    switch(action.type) {
        case "CHANGE_COUNT":
            return {
                ...state,
                count: state.count + action.payload
            }
        case "ADD_FAVORITE_THING":
            return {
                ...state,
                favoriteThings: [...state.favoriteThings, action.payload]
            }
        default:
            return state
    }
}
```

Using array methods within the cases of a switch statement:

```js
case "REMOVE_FAVORITE_THING": {
	const arrCopy = [...state.favoriteThings]
	
	const updatedArr = state.favoriteThings.filter(thing => thing.toLowerCase() !== action.payload.toLowerCase())
	return {
		...state,
		favoriteThings: updatedArr
	}
}
```

Cases that change a more complex state with many object layers. Note the `...` on multiple lines:

```js
const initialState = {
    count: 0,
    favoriteThings: [],
    youtubeVideo: {
        title: "",
        viewCount: 0,
        votes: {
            up: 0,
            down: 0
        }
    }
}

case "SET_YOUTUBE_TITLE":
	return {
		...state,
		youtubeVideo: {
			...state.youtubeVideo,
			title: action.payload
		}
	}
case "UPVOTE_VIDEO":
	return {
		...state,
		youtubeVideo: {
			...state.youtubeVideo,
			votes: {
				...state.youtubeVideo.votes,
				up: state.youtubeVideo.votes.up + 1
			}
		}
	}
```

## Combine reducers

Multiple reducer functions are set up on different files with their own action creators, like you would with componenets. Everything is placed in a redux folder, and it is convention to have an index.js file that imports all the different reducers and combines them into a single state tree.

CombineReducers() takes an object that represents the structure of the initial state object, and that becomes the state of the whole application. See project redux-plain-js-practice for entire project example.

## Redux in React

Redux is imported in the main index.js file in React using a provider imported from react-redux. The store needs to be imported next from the index.js in the redux folder.

```js
import React from "react"
import ReactDOM from "react-dom"
import {Provider} from "react-redux"
import store from "./redux"
import App from "./App"

ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>, 
    document.getElementById("root")
)
```

## connect()

Connect() is a higher order component that returns a function, which is passed the entire App as a parameter.

```js
// what connect expects
export default connect(/* What parts of state do you want? */, /* What actions to dispatch? */)(App)

// function and object to pass to connect()
function mapStateToProps(state) {
    return {
        count: state
    }
}

const mapDispatchToProps = {
    increment: increment,
    decrement: decrement
}

export default connect(mapStateToProps, mapDispatchToProps)(App)

// one liner
export default connect(state => ({count: state}), {increment, decrement})(App)
```

## useSelector and useDispatch

The hooks useSelector() and useDispatch() replace connect().

```js
function App(props) {
// takes a function as a parameter to select the state in use
    const count = useSelector(state => state)
// dispatcher for actions
    const dispatch = useDispatch()
    return (
        <div>
            <h1>{count}</h1>
            <button onClick={() => dispatch(decrement())}>-</button>
            <button onClick={() => dispatch(increment())}>+</button>
        </div>
    )
}
```
