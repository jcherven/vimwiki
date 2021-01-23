# Number functions and Math class methods for JS

## Builtin functions for numbers

### parseInt() (non-mutating)

`parseInt(string)` Returns an int value of `string`. Radix is an optional arg that specifies the base of the returned int.

parseInt does not default to base 10 if the radix arg is not provided. In this case, it's simply type coerced into a `number`.

### parseFloat(string)

### isNaN(value)

Returns a boolean; `true` if the value is not a number.

### eval(string)

Runs `string` with all of the privileges of the caller. Very dangerous.

A sane alternative to `eval()` is `window.Function()`.

## Math Class Static Methods

### Math.random()

Returns a random `float` bewteen 0 and 1.

### Math.max(values)

Takes values as arguments. A deconstructed array can be passed in with the spread operator:

```javascript
let vTuberRanking = [300, 238, 1004, 93];
Math.max(...vTuberRanking);
// 1004
```

### Math.min(values)

Works like `Math.max()`

### Math.round(x)

Returns the closest int

### Math.floor(x)

Rounds down to the integer

### Math.ceil(x)

Rounds up to the integer

### Math.truc(x)

Non rounding, just cuts off any points behind the decimal.

### Math.abs(x)

### Math.sign(x)

Returns 0, 1, or -1 for the sign of the number passed in.

### Math.pow(x, y)

Returns a x^y as a number.

### Math.sqrt(x), Math.cbrt(x)

### Math.exp(x), Math.log(x)

returns e^x and log x

## Math Class Static Properties

The Math class contains some useful static properties for common numbers like `Math.PI`.

[Math Class MDN documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)

