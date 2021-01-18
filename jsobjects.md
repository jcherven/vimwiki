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

