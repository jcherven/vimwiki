# JS Arrays

In js, arrays are dynamic:
- they don't need you to specify how much data to hold
- they can be of arbitrary mixed data types (values, strings, objects, bools, etc)

```javascript
// for instance, this is a valid array in js
let absoluteGarbage = [ 12, 'pekora', true, null, NaN ];
```

```javascript
// other ways an array can be instantiated
new Array()
// []
[]
// []
```

- strings will be instantiated as immutable arrays
- strings inherit array methods but also define their own special methods like `trim()`, `concat()`, etc.
- strings can be accessed by index, but can't be changed (without creating a new array)

## Arrays as References

Variables referencing arrays are always references in js. This gives arrays their mutability and enables the functionality of the array methods below.

Arrays declared with `const` can be mutated, unlike value types decalred with `const`. Generally, a new declared array should be done with `const` in a lot of cases. 

## Mutating Arrays

- indexes can be added to arrays arbitrarily

```javascript
> let list = [];
// skipping the first two indices of list[].
> list[2] = 'basil'
// 'basil'
> list
// [ <2 empty items>, 'basil' ]
```

## Array Methods

### includes(), indexOf() Search Methods

- `array.includes(value, [fromIndex])`: finds an exact match of `value`, returns a boolean
	- has an optional fromIndex argument:
		- `array.includes('megurine luka', 3)` searches the value 'megurine luka' after index 3 onwards

- `array.indexOf(value, [fromIndex])`: finds an exact match of `value`, returns the index number of `value`
	- has an optional fromIndex argument:
		- `array.indexOf('morfonica', 6)` searches after index 6 (inclusive)

### push(), pop() Postfix Methods (mutating)

These will mutate the array.

- `array.push(value)`: adds `value` to end, returns the new length
- `array.pop(value)`: removes `value` from end, returns the popped value 

Consider this way of doing things:

```javascript
let korosanWords = ['yubi', 'oayo', 'horayo'];
// this behaves exactly like push() with a single value passed in
korosanWords[korosanWords.length] = 'chikisho';
```

### unshift(), shift() Prefix Methods (mutating)

These will mutate the array

- `array.unshift(value, [value], [...])`: adds to the beginning, returns the unshifted new length
	- mnemonic: think of the array shifting right, making space for the passed arg
- `array.shift(value, [value], [...])`: removes from the beginning, returns the shifted value
	- mnemonic: think of the array shifting left, dropping off the first value.
- multiple values can be passed into unshift and push. new items get inserted in the order they're passed.

	```javascript
	let korosanWords = ['yubi', 'oayo'];
	korosanWords.unshift('chikisho', 'horayo');
	// [ 'chikisho', 'horayo', 'yubi', 'oayo' ]
	```

### concat() (non-mutating)

Merges two or more arrays. Does not mutate the array.

```javascript
const track1 = ['roselia', 'determination symphony'];
const track2 = ['afterglow', 'sen sen fukoku'];

array1.concat(array2);
// ['roselia', 'determination symphony', 'afterglow', 'sen sen fukoku']
// track1 has not been mutated by this
```

### join() (mutating)

- `array.join(delimiter)` mutates `array`, turning it into a string object with the delimiter:
	- numbers and other types like floats will be turned into string literals
 
	```javascript
	let letters = [ m, i, k, u ];
	letters.join();
	// "m,i,k,u"
	```
	
	```javascript
	let letters = [ m, i, k, u ];
	letters.join('');
	// "miku"
	```
	
	```javascript
	let letters = [ m, i, k, u ];
	letters.join('-');
	// "m-i-k-u"
	```
	
	```javascript
	// non string datatypes
	let numbers = [ 12.3, 60, false ];
	letters.join('-');
	// "12.3-60-false"
	```

### slice() (non-mutating)

This does not mutate the array.

- `array.slice(value)` captures a subarray from `value` to the end of the array (without mutating `array`)
- `array.slice(5)` will return `array` elements starting from index 5
- `array.slice(startIndexInclusive, endIndexExclusive)` captures a subarray without mutating `array`:
	- the start index is inclusive
	- the end index is exclusive

	```javascript
	let band = ['vocal', 'guitar1', 'bass', 'guitar2', 'drums', 'keyboard']
	let stringInstruments = band.slice(1,4);
	// ['guitar1', 'bass', 'guitar2']
	```
	- `array.slice(-3)` is valid, it will return the last 3 items of `array`
	- `array.slice(-3, -2)` captures the subarray of the third-last to second-last items.
- `array.slice()` with no arguments simply copies the array. It is useful and will appear in a lot of code.

### splice() (mutating)

This mutates the array. It's used for arbitrarily changing the contents of an array.

`array.splice(start[, deleteCount[, item1[, item2[, ...]]]])`

- Splice returns an array of deleted items. Nothing is returned if nothing is deleted.
	- Thus, splice can be used to both edit the array and get any removed items at once.
- The start argument value is the item count (non-inclusive), not the array's index number.
- The deleteCount argument is a number of items to be deleted
- Deleted items don't leave empty indexes in the array. You get a new contiguously populated array.
- Omitting replacement args simply deletes the targeted items. The deleted items are returned and the array is now shorter.

- `array.splice(3, 0, 'koro')` will insert the string 'koro' at index 4 of `array`. Nothing is returned.
- `array.splice(1, 2, 'oka')` will replace item 2 and 3 (indexes 1, 2) with the value 'oka'. An array with items 2 and 3 are returned.
- `array.splice(1, 2)` will simply delete the items 2 and 3 (Array indexes 1 and 2).

Consider this way of changing a single item in an array:

```javascript
let roselia = ['yukina', 'lisa', 'rinko', 'saya', 'ako'];
let keyboardist = 'rinko';

roselia.splice(roselia.indexOf(keyboardist), 1, keyboardist.toUpperCase());
// ['rinko']

> roselia
// [ 'yukina', 'lisa', 'RINKO', 'saya', 'ako' ]
```

### reverse() Sorting method (mutating)

- `array.reverse()` mutates `array`, reversing the index order as a return value.

### sort() Sorting method (mutating)

- array.sort() mutates `array`. The default (no args) sort order is tricky; numbers are converted to strings and the array is sorted by the UTF-16 values.
- The effect of this is that strings will be alphabetically sorted, while numbers will have a strange ordering.
- A sorted array is returned.
- `array.sort()` 

