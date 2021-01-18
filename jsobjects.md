# JS Objects

## Keys and Symbols

In js, object property keys are converted to strings.

```javascript
const raiseASuilen = {
	1001: 'Layer',
	1002: 'Pareo',
	1003: 'Chu2',
	1004: 'Masking',
	1005: 'Lock'
}
```

The node interpreter demonstrates this:

```javascript
> raiseASuilen
// { '1001': 'Layer', '1002': 'Pareo', ... }
```

Object keys that are string literal numbers have to be accessed by symbol using square brackets:

```javascript
// this doesn't work
> raiseASuilen.1001
// Uncaught SyntaxError: Unexpected Number

// accessing the value by symbol works
> raiseASuilen[1001]
// "Layer"

// this is however not an index identifier
> raiseASuilen[2]
// undefined
```

Dot notation will attempt to access the string literal of the property. To use a variable for accessing the object, the property has to accessed by symbol. The square bracketed part is an expression that will be evaluated.

```javascript
const afterglow = {
	vocal: 'ran',
	bass: 'himari',
	guitar1: 'ran',
	drum: 'tomoe',
	keyboard: 'tsugumi',
	guitar2: 'moca',
}

let instrument = "drum";
```

```javascript
> afterglow.instrument
// undefined

> afterglow[instrument]
// 'tomoe'
```

## Builtin Object Properties

Js objects have data properties and accessor properties.

### Data properties

- `[[Configurable]]` a boolean that sets whether a property can be redefined or removed (via `delete` operator)
- `[[Enumerable]]` a boolean that sets whether or not a property can be returned in the `for...in` loop
- `[[Writable]]` a boolean that sets the mutability of a property
- `[[Value]]` contains the value of the property. It gets a default value of `undefined`.

The boolean properties are defaulted to false when the `Object.defineProperty()` is used to create the property. Otherwise, they are usually set true.

### Accessor properties

-

## Builtin Object Methods

### Object.keys(obj)

`Object.keys(vocaloid)` returns a list of keys in the object `vocaloid` as an array.

### Object.values(obj)

`Object.values(vocaloid)` returns a list of values in the object as an array.

### Object.entries(obj)

`Object.entries(vocaloid)` returns an array where each key-value pair is a subarray.

```javascript
const vocaloid = { name: "Megurine Luka", hairColor: "pink", module: "New Year" }

Object.entries(vocaloid)
// [["name", "Megurine Luka"], ["hairColor", "pink"], ["module", "New Year"]]
```

### Object.fromEntries(array)

`Object.fromEntries(megurineLuka)` will return an object from the passed in array where each subarray make up the new objects key-pair values. See Object.entries(obj) above.

### Object.assign(target, source) (mutating)

This will mutate the object `target`.

`Object.assign(target, source)` copies all enumerable own properties into a target object into one or more source objects. You get a new object with the new properties added.

```javascript
const memberProfile = { name: "ran", band: "afterglow" }
const cardMeta = { type: "powerful", stars: 4 }

const newCard = Object.assign(ranCard, cardMeta);
// Object { name: "ran", band: "afterglow", type: "powerful", stars: 4 }
```
