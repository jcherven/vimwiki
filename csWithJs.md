# CS stuff in JS

## parameters, arguments

	- signature: part of a method's definition that specifies what variables will be used in the call
	- parameter: a variable which is part of a method's signature
	- argument: an expression or value that's passed into a method

## Generalized functions

```javascript
function tenSquared() {
	return 10 * 10;
}
```

this is not a generalized function because it will always return one value. it's beyond useless because it breaks the soft rules of repeating code. at this point it may as well be a static variable, which takes far less memory. better yet, it can be an expression, but even then it's a waste of compute time.

```javascript
function squareNum(num) {
return num * num;
}
```

this is slightly better, since it will accept any int value and do something deterministic to produce a computed value. the return value is TBD by the input. still, this isn't fully generalized. instead of simply squaring, how about any arbitrary power operation? we can make the code itself TBD by a power parameter so that powers other than 2 can be computed.

```javascript
function power(num, pow) {
	let answer = 1;
		for (i = 1; i <= pow; i++) {
			answer *= num;
		}
	return answer;
}
```

this is probably sufficiently generalized. now any int value can be multiplied by itself any number of times. of course, this can be further generalized to other math computations by allowing it to accept an operator, which would allow it to compute more than simply powers of numbers. but to generalize powers of numbers, this is as general as it gets.

## repeating functionality

```javascript
function copyArrayAndMultiplyBy2(array) {
	const output = [];
	for (let i = 0; i < array.length; i++) {
		output.push(array[i] * 2);
	}
	return output;
}

const myArray = [1, 2, 3];
const result = copyArrayAndMultiplyBy2(myArray);
```

in the global context, we're storing this function. in the same context, a reference to an array is defined as `myArray`. then a reference to a function call is assigned to `result`. since this references a function call, result is evaluated in a new execution context on the top of the call stack, inside which the function runs. when the return value is computed, the function call's context pops off the stack with the value of the global constant `result`, bringing the thread of execution back into the global context.

```javascript
function copyArrayAndDivideBy2(array) {
	const output = [];
	for (let i = 0; i < array.length; i++) {
		output.push(array[i] / 2);
	}
	return output;
}

const myArray = [1, 2, 3];
const result = copyArrayAndDivideBy2(myArray);
```

here we are doing almost the same thing as copyArrayAndMultiplyBy2(). it's a good sign that this can be generalized, but this computation is a little more complex. a good way to handle the complexity is to let one of the parameters be another function that will be used to get the result you want.

```javascript
function copyArrayAndManipulate(array, instructions) {
	const output = [];
	for (let i = 0; i < array.length; i++) {
		output.push(instructions(array[i]));
	}
	return output;
}

function multiplyBy2(input) { return input * 2; }

const myArray = [1, 2, 3];
const result = copyArrayAndManipulate(myArray, multiplyBy2);
```

here we're composing functions in a very flexible way. we've defined a custom function `multiplyBy2()` that can be used as an arg in the call to `copyArrayAndManipulate()`, which is being used as a framework for doing anything you want to each element of any array (immutably, even). that's a higher order function. ES6 has a bunch of these higher order functions for various classes, like Array's map(), reduce(), forEach(), and so on.


