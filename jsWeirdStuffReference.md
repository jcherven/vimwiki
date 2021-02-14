# javascript idiosyncrasies

these kinds of things tend to improve the legibility of the code, but not necessarily the readability. in other words, they help developers familiar with js syntactic sugar to know what's happening without digging though lots of other code, but they are less self-descriptive to someone not familiar with the syntactic sugar.

## arrow functions

```javascript
function multiplyBy2(input) { return input * 2; }
const muliplyBy2 = (input) => { return input * 2; }
const multiplyBy2 = (input) => input * 2
const multiplyBy2 = input => input * 2
const output = multiplyBy2(3)
//> 6
```

## anonymous functions

```javascript
function copyArrayAndManipulate(array, instructions) {
	const output = [];
	for (let i = 0; i < array.length; i++) {
		output.push(instructions(array[i]));
	}
	return output;
}

// running the higher order function with an anonymous function
const result = copyArrayAndManipulate( [1, 2, 3], input => input * 2 );
// anonymous function defined here ------------->[                 ]
```

know that due to lexical scope, arrow functions and anonymous functions are not suitable for general function definitions.

## lexical (static) scope



## Closure

1. each time a function is invoked, its object gets a new instantiation and thus new local memory. when it returns a value to its calling context, popped from the call stack, and its local memory is lost.
2. there are times when a function invocation would need to be re-used with the data it's already been given.
3. to do so, one way is to have it return a function to the global execution context, where its local data can continue to be used after the original call to it has returned and popped off the call stack.

```javascript
function createFn() {
	function multiplyBy2(num) {
		return num * 2;
	}
	return multiplyBy2;
	// javascript won't evaluate multiplyBy2 because this isn't a call. a call to be evaluated would have parens.
}

const generatedFn = createFn();
const result generatedFn(3);
```

in createFn(), the code of multiplyBy2() gets stored in global memory after createFn() returns. this turns the identifier `result` effectively into a command to run that code. however, the code referenced by `result` has nothing to do with the original function call. saving a function in global memory like this allows it to gain a powerful ability to use data in the *global context*, which was previously off limits.

```javascript
function outer() {
	let counter = 0;
	function incrementCounter() {
		counter++;
	}
	incrementCounter();
}

outer();
```

this is valid code, and the counter++ expression is able to use the variable counter declared outside its execution context.

incrementCounter()'s execution context is inside outer()'s execution context. in its own local memory, the counter++ expression does not have the value of counter. in js, it appears as if the value is allowed to be looked up in the outer context.

```javascript
function outer() {
	let counter = 0;
	function incrementCounter() { counter ++; }
	return incrementCounter;
}

const myNewFn = outer();
myNewFn();
myNewFn();
```

on the first call to `myNewFn()`, a new execution context is pushed onto the call stack. the code of that function is stored in global memory as the data referenced by `myNewFn`. when that code is run, you'd expect the `counter ++` expression to look outside to the calling execution context to find the value of `counter` is missing since `counter` was destroyed along with outer()'s execution context, yet the code still works. it turns out that js wrote a copy of outer()'s local memory out to global memory inside of a hidden property of myNewFn. 

on the second call, the same area of global memory is referenced, but in a new execution context. within that code's memory space, the same value for counter is incremented again. this can be verified in the console by running `console.dir(myNewFn)` and inspecting the hidden object property called `[[scope]]`. since the object for myNewFn has a `[[scope]]` property, it knows to look in there for the value of counter. after returning incrementCounter, this context is popped off the call stack. myNewFn remains as data in global memory with the new value of `counter`. access to this data is restricted such that only further calls to myNewFn() will be able to get or set the data. this has given us permanent, private state for this function.

## technical definition

both the overall concept of this, and the special property being stored, is called closure. colloquially we'd say "the data is in the function's closure", which is to say that the data is in the `[[scope]]` hidden property of the function's object in global memory.

js has a particular scope rule called lexical (or static) scoping. this means that data available to a function is determined where in memory that function is stored rather than where it's called from. the latter is known as dynamic scoping.

## multiple closures

if a new const is declared with a call to outer, that new const gets its own new function in global memory, and that function object has its own closure.

```javascript
const newFn = outer();
const anotherFn = outer();
// these two will each have their own closures.
```

## practical uses

	- helper functions like `once` and `memoize`
	- iterators and generators which use lexical scoping and closure to achieve the most contemporary patterns for handling data in js
	- module pattern, which preserves the state for the life of an application without polluting the global namespace
	- asynchronous javascript with callbacks and promises rely on closure to persist state in an async environment


