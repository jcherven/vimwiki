# React Component Lifecycle

These are listed in the order they are called when a component object is initialized.

There are three rarely used lifecycle methods that aren't listed here: `shouldComponentUpdate()`, `getDerivedStateFromProps()`, and `getSnapshotBeforeUpdate()`. they are important but not for making most components.

## Actual lifecycle

- Mounting
	- `constructor()`
	- `static getDerivedStateFromProps()`
	- `render()`
	- `componentDidMount()`
- Updating
	- `static getDerivedStateFromProps()`
	- `shouldComponentUpdate()`
	- `render()`
	- `componentDidUpdate()`
- Unmounting
	- `componentWillUnmount()`
- Error Handling
	- `static getDerivedStateFromError()`
	- `componentDidCatch()`

## 0. `constructor(props)` (optional)

React component constructors are for:

1. initializing local state by assigning an object to `this.state`
2. binding event handler methods to an instance

they are optional if you don't bind methods or don't initialize state.

the constructor is the only place where state should be directly manipulated (all other state manipulations should be done with the `setState()` method).

if state is directly assigned, `super(props)` must be called. failing to do so will cause `this.props` to be `undefined`.

```javascript
constructor(props) {
	super(props);
	this.state = { anyNumber: null, funnyName: '' };
}
```

State can also be set outside the constructor by instantiating a state object:

```javascript
class App extends React.Component {
	state = { anyNumber: null, funnyName: '' };
	// ...rest of the component code
}
```

State should not, however, ever be updated by direct manipulation of `this.state` outside of the constructor. The only time `this.state` can be safely manipulated is when instantiating a state object. Manipulations should be done with the `setState()` method.

## 1. `render()` (required)

`render()` is the only required method in a class component. the implementation of the function should be a "pure function", meaning that it does not modify component state, it returns the same result each time it's invoked, and it has no side effects.

if we look strictly at the most fundamental thing the render method does, it simply returns something to be used in the DOM. it must return some type based on what it finds in its examination of `this.props`. One of the most common types is a React element (JSX) for rendering a DOM node, but other types include JS values (as text DOM content) and some special react data types ([fragments](reactFragments), [portals](reactPortals))

the best way to keep the `render()` method pure is to avoid manipulating the browser with it. other lifecycle methods are responsible for that.

### `render()` trivia

- `render()` will not be invoked if `shouldComponentUpdate()` returns `false`

## 2. `componentDidMount()`

this is one of the methods in which it's okay to interact with the browser. it only runs once after the `render()` method, so it's great for things like initial state loading. official docs prefer doing setup operations like data loading in here rather than in the constructor. setup code will work in the constructor, but it's preferred to do it here for reasons that i have not investigated yet.

## 3. `componentDidUpdate()`

A very simplistic way to look at what a component is doing while a user is viewing a page of the app is to imagine it waiting for a state update. 
gets called anytime there is a change like change in state or a new set of props being passed from the parent. examples include making a request on click or live seach help while the user types.

## 4. `componentWillUnmount()`

not sure about this one yet. it apprently does some cleanup.

