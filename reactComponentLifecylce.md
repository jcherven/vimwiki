# React Component Lifecycle

These are listed in the order they are called when a component object is initialized.

There are three rarely used lifecycle methods that aren't listed here: `shouldComponentUpdate()`, `getDerivedStateFromProps()`, and `getSnapshotBeforeUpdate()`. they are important but not for making most components.

## 0. `constructor(props)` (optional)

optional, because react's app component prototype will deal with constructors. state can be set in the constructor if needed. the constructor is the only place where state should be directly manipulated (all other state manipulations should be done with the `setState()` method).

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

## 1. `render()`

if we look strictly at the most fundamental thing the render method does, it simply returns JSX. this method is required, and it must return some JSX.

## 2. `componentDidMount()`

this is a perfect time to do some initial data loading for the component. it only runs once after the render() method, so it's great for things that need to only run once. official docs prefer doing setup operations like data loading in here rather than in the constructor. setup code will work in the constructor, but it's preferred to do it here for reasons that i have not investigated yet.

## 3. componentDidUpdate()

gets called anytime there is a change like change in state or a new set of props being passed from the parent. examples include making a request on click or live seach help while the user types.

## 4. componentWillUnmount()

not sure about this one yet. it apprently does some cleanup.

