# javascript idiosyncrasies

## destructured objects

```javascript
const person = {
	firstN: 'Pekora',
	lastN: 'Usada',
	generation: '3rd',
	catchphrase: 'Konpeko x3',
	greeting: 'Dou~mo dou~mo',
	printGreeting() {
		// destructuring 'this' so that the properties can be used without the 'this' keyword.
		// question: what does this have to do with scope and this object's context?
		const {
			firstN,
			lastN,
			generation,
			catchphrase,
			greeting
		} = this;
		console.log(`${catchphrase}! It's Hololive ${generation} generation's ${lastN} ${firstN} peko! ${greeting}!`)
	}
}
```

## behavior of the keyword `this`

The Window class is instantiated as the global scope of the browser. When you define functions and variables in the global scope, they are added to current Window object as properties. Therefore, `this` in the global execution context will be a Window object.

### invocation context

the value of `this` depends on the invocation context of the function in which it is used. 

```javascript
const chao = {
	type: "mischevious",
	color: "violet",
	nickName: "gremlin",
	printBio() {
		const { type, nickName, color } = this;
		console.log(`${nickName} is a ${color} ${type}-type chao.`)
	}
}

// invoking printBio like so will make this run in the context of the calling object (global)
const printBio = chao.printBio;
printBio();
// > TypeError: this.nickName is not a function

// invoking printBio like this will run it in chao's context, and `this` will work.
chao.printBio()
// > gremlin is a violet mischevious-type chao.
```

## computed object properties

Dynamic object properties are now available in js.

This is the expected behavior of attempting to define a property with a variable.

```javascript
const instrument = 'drums';
const member = 'Masuki Sato';

const band = {
	instrument: member
}

console.log(band);
// > {instrument: "Masuki Sato"}
```

The property identifier will take the literal string "instrument". If we'd like the value of the variable `instrument`, this square bracket syntax would be used:

```javascript
const instrument = 'drums';
const member = 'Masuki Sato';

const band = {}
band[instrument] = member;

// > band
// > {drums: "Masuki Sato"}
```

Alternatively:

```javascript
const band = {
	[instrument]: member
}
```

Any valid expression can be evaluated.

```javascript
function addProp(obj, key, val) {
	const copy = {
		...obj,
		[key]: val,
	};
	return copy;
}

const res = addProp(band, 'affinity', 'cool');

// > res
// > {drums: "Masuki Sato", affinity: "cool"}
```

Any valid expression.

```javascript
const newCard = { [Math.round(Math.random() * 100)]: 'Masuki Sato' }
// > newCard
// > {63: "Masuki Sato"}
```

## arrow functions (arrow function expressions, lambda expressions)

Due to lexical scoping, the `this` property of a method defined with an arrow function expression uses the calling context's `this`. The following won't work because `this` will refer to the calling context:

```javascript
const chao = {
	name: 'warachao',
	laugh: () => {
		console.log(`${this.name} goes lol`)
	}
}

chao.laugh()
// > undefined goes lol

```

If the calling context has a `name` reference, that one will be used.

The exceptions of arrow function expressions are the following:

- no bindings to `this` or `super`, and therefore should not be used as methods.
- no `arguments` or `new.target` keywords
- not suitable for `call`, `apply`, and `bind` methods, as these rely on establishing a scope (will probably cause runtime errors)
- can not be used as constructors (will throw an interpreter error)
- can not use `yield` within its body.

### leveraging arrow function expressions and `this`

```javascript
const autoChao = {
	phrases: ["chaochao", "ch-chao", "*blinks*", "*looks interested in what you're holding*", "CHAO"],
	pickPhrase() {
		const { phrases } = this;
		const idx = Math.floor(Math.random() * phrases.length);
		return phrases[idx];
	},
	start() {
		setInterval(function () {
			console.log(this.pickPhrase());
		}, 3000)
	}
}

autoChao.start();
// this is broken
```

The call to autoChao.start() is in the global execution context. Since start contains code that calls setInterval(), that call will reference `this` as the window object.

An arrow function does not have `this`, and therefore it will reference the execution context of `start()`, which does have access to the pickPhrase method.

```javascript
// ...
start() {
	setInterval(() => {
		console.log(this.pickPhrase())
	}, 3000)
}
// ...

autoChao.start();
// this works as expected
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
// anonymous function defined here ------------->[                  ]
```

know that due to lexical scope, arrow functions and anonymous functions are not suitable for general function definitions.

## lexical (static) scope

js has a particular scope rule called lexical (or static) scoping. this means that data available to a function is determined where in memory that function is stored rather than where it's called from. the latter is known as dynamic scoping.

the term lexical refers to the fact that one can derive the scope by reading the source code. another way to think about this is that the scope for a function can be deduced at compile time.

## closure

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
const result = generatedFn(3);
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

### multiple closures

if a new const is declared with a call to outer, that new const gets its own new function in global memory, and that function object has its own closure.

```javascript
const newFn = outer();
const anotherFn = outer();
// these two will each have their own closures.
```

### practical uses

	- helper functions like `once` and `memoize`
	- iterators and generators which use lexical scoping and closure to achieve the most contemporary patterns for handling data in js
	- module pattern, which preserves the state for the life of an application without polluting the global namespace
	- asynchronous javascript with callbacks and promises rely on closure to persist state in an async environment

## hoisting

hoisting is a behavior particular to js in which declared identifiers are initialized before the code is run.

```javascript
console.log(yubi);
var yubi = 55;
// undefined

scream()
function scream() { console.log("yubi yubi"); }
// the interpreter hoists scream() and runs without scream being defined before calling.
```

rather than producing a missing reference error, the console understands that `yubi` is initialized somewhere in the script, but does not define it until the line where `yubi` is assigned to the value 55. this is a side effect of how function definitions are treated in many other languages as well as JS, where function calls can occur before the function definition in otherwise sequentially written code.

identifiers declared with `var` are hoisted by the interpreter, while those declared with `let` and `const` are not. in the cases of these keywords, a reference error is produced. in the same manner as with values, plain function declarations are hoisted, and function expressions of `var` are hoisted as well. however, function expressions of `let` and `const` are not hoisted. one of the key features of let and const keywords is that they prevent this hoisting side effect in order to prevent sneaky bugs.

## async javascript

```javascript
console.log('yubi yubi');

setTimeout(function() {
	console.log('bye bye');
}, 3000);

console.log('horayo');
console.log('mogu mogu');
console.log('dou~mo dou~mo');
```

`setTimeout`'s callback function runs asynchronously here. the string `bye bye` will print last in the console. the 

### the callback pyramid

assume we'd like to animate a button to move across the page, and we've decided to do this by translating it to the right by 100px every second. This will move the button 100px to the right exactly once. Repeating the action requires nested setTimeout calls.

```javascript
const btn = document.querySelector('button');

setTimeout( () => {
	btn.style.transform = `translateX(100px)`;
	setTimeout( () => {
		btn.style.transform = `translateX(100px)`;
			setTimeout( () => {
				btn.style.transform = `translateX(100px)`;
			}, 1000 );
	}, 1000 );
}, 1000 );

```

Consider a way to do this instead with a function that accepts callback input.

```javascript
const moveX = (element, amount, delay, callback) => {
setTimeout( () => {
	elements.style.transform = `translateX(${amount}px)`
	callback();
}, delay )
}

moveX(btn, 100, 1000, () => {
	moveX(btn, 200, 1000, () => {
		moveX(btn, 300, 1000, () => {
			moveX(btn, 400, 1000);
		});
	});
});
```

Callback functions are marginally more readable in this case, but completely unhelpful if they contain any significant amount of code. To avoid this pattern, Javascript Promises are used to chain asynchronous code. However, understanding this pattern is helpful in understanding what Promises are.

## Promises (the Promise class)

### Overview

Rewriting the above with promises looks like this:

```javascript
moveXPromise(btn, 100, 1000)
	.then( () => moveXPromise(btn, 200, 1000))
	.then( () => moveXPromise(btn, 300, 1000))
	.then( () => moveXPromise(btn, 400, 1000))
	.catch(( position ) => {
		alert('screen boundary reached');
	});
```

Exception handling was even thrown in for free. This is much more descriptive and readable.

### Instantiating a new Promise

```javascript
new isKoroneStreaming = new Promise((resolve, reject) => {});
```

Promise's constructor accepts callback functions for the eventualities of the states `resolved` and `rejected`. This state is kept in a hidden property of the object, `[[PromiseStatus]]`.

### Calling a Promise

Promise also has the methods `then()` and `catch()` to handle the states `resolved` and `rejected` respectively.

```javascript
const isKoroneStreaming = new Promise((resolve, reject) => {
	let streaming = Math.random();
	streaming < 0.5 ? resolve() : reject();
});

isKoroneStreaming
	.then(() => { watchLive(); })
	.catch(() => { watchArchive(); })
```

Before resolving or rejecting, `[[PromiseStatus]]`'s value will be `pending`, such as in the case of waiting on a web request to resolve.

Consider instantiating the promise as the return in a function expression to take advantage of closure:

```javascript
// instantiation
const promiseToWatchKorone = () => {
	return new Promise((resolve, reject) => {
		checkKoroneStatus((isStreaming) => {
			isStreaming ? resolve(streamUrl) : reject(archiveUrl);
		});
	});
};

// call
promiseToWatchKorone()
	.then ((streamUrl) => { watchLive(streamUrl); })
	.catch ((archiveUrl) => { watchArchive(archiveUrl); })
```

Many request libraries like Axios use functions that return promises like this.

### Chaining multiple promises

With web requests, common pattern is to chain promises to make followup requests using data gotten from a previous request. As long as a request returns a promise object, `.then()` can be chained sequentially.

Here, assume `fakeRequest()` returns a promise. We'll request a user id, then use that data to hit the endpoint again for getting that user id's top post.

```javascript
fakeRequest('/users')
	.then((res) => {
		const id = res.data[0];
		return fakeRequest(`/useasds/${id}`)
	})
	.then((res) => {
		const postId = res.data.topPostId;
		return postId;
	})
	.catch((err) => {
		return err;
	});

```

The `catch` will run if anything in the chain is rejected.
