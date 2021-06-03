# CSS Rendering

HTML is parsed by the client to produce the DOM. CSS is parsed to produce the CSSOM. These are combined to produce the Render Tree. Using the Render Tree, the client generates the visual formatting model which will produce the window contents.

## Establishing some terms of CSS

This is a selector with an empty declaration block:
```
.this-class {}
```

A CSS Rule is a selector with a declaration block. Each statement in there is a declaration:
```css
.my-class {
	color: blue;
	text-align: center;
	font-size: 30px;
}
```

Declarations are composed of a property and a declared value.

## Two main operations of CSS parsing

The CSSOM is produced after two main operations: the cascade and value processing.

### Cascade (Resolution of conflicting CSS declarations)

#### The Cascade

This is the process of combining different stylesheets and resolving conflicts between different CSS rules and declarations when more than one rule applies to a certain element.

The default set of CSS rules applied by the browser are the User Agent rules. The user of the client can define the User rules. The web page author writes the Author rules. The cascade resolves conflicts between these sources so that everyone's definitions get used, but there is an order of precedence for CSS rules. The cascade calculates this precedence according to importance, specificity, and source order.

##### Importance

The most general hierarchy in the cascade is ordered like this:

1. User `!important` declarations
2. Author `!important` declarations
3. Author declarations
4. User declarations
5. User Agent declarations

##### Specificity

Conflict resolution for similar importance is done with specificity.

1. Inline styles
2. IDs
3. Classes, pseeudo-classes, attribute
4. Elements, pseudo-elements

Consider these author declarations, which all have the same importance.

```css
.button {
	font-size: 20px;
	color: white;
	background-color: blue;
}

/***
Each item is counted. In this rule, there are:

- Inline: 0
- IDs: 0
- Classes: 1
- Elements: 0
***/

nav#nav div.pull-right .button {
	background-color: green;
}

/***
- Inline: 0
- IDs: 1
- Classes: 2
- Elements: 2
***/

a {
	background-color: purple;
}

#nav a.button:hover {
	background-color: yellow;
}
```
##### Source Order

### Processing of final CSS calues
