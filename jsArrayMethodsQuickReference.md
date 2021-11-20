# JS Array Methods Quick Reference

## Array.prototype.reduce()

Required arguments:
- `callbackFn`
Optional arguments:
- `initialValue`
	- This will be the value that `callbackFn` uses as its required `initialValue` arg on the first iteration

`callbackFn` required args:
- `previousValue`
- `currentValue`
`callbackFn` optional arguments:
- `currentIndex`
- `array`

### Examples
```javascript
[3, 5, 7, 9, 11].reduce((accumulator, currentValue) => {
	return accumulator + currentValue;
}, 0);
```
## Array.prototype.every()

Required arguments:
- `callbackFn`
	- `element` (required)
	- `index` (optional)
	- `array` (optional)
Optional arguments:
- `thisArg` (a value to use as `this` when executing `callbackFn`)

### Examples
```javascript
const words = ["dog", "dig", 'log', 'bag', 'wag'];
```

```javascript
words.every(word => {
return word.length === 3;
});
// returns true
```

```javascript
words.every(word => word[0] === 'd');
// returns false
```

```javascript
words.every(w => {
	let last_letter = w[w.length - 1];
	return last_letter === 'g'
});
// returns true
```
