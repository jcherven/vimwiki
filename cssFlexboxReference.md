# CSS Flexbox Reference

[w3.org flexbox docs](https://www.w3.org/TR/css-flexbox/#box-model)

## The Flex Layout Model

Flex containers are set with the `display: flex|inline-flex;` declaration. In-flow children of a flex container are called **flex items** and are laid out using the flex layout model.

An element having the `display` value of `flex` will flow as a block level element. A value of `inline-flex` will behave as named.

`flex-direction` declares the orientation of the flex layout. The default is `flex-direction: row`, and this is applied if not specified.

## Flex Property Shorthand

The `flex:` property shorhand is written with the order of:
1. **flex-grow**: the grow factor of a flex item's main size. Defaults to `0`.
2. **flex-shrink**: the shrink factor of a flex item's main size. If all items are larger than the flex container, items shrink according to this. If `0`, items will not shrink at all and can overflow the container. Defaults to `1`.
3. **flex-basis**: the initial size of a flex item. It sets the size of the content box, unless otherwise set with `box-sizing:`. Defaults to `auto`.

```css
.container { display: flex; }

.item {
	flex: 0 1 auto;
}

.redundant-item {
	flex-grow: 0;
	flex-shrink: 1;
	flex-basis: auto;
}
```

## Flexbox patterns

### Vertical centering

In the flex item, specify dimensions and set the margin to `auto`.

```css
.container {
	display: flex;
}

.container > div {
	width: 100px;
	height: 100px;
	margin: auto;
}
```

### Vertically Centered Items

The `align-items` property deals with the **cross axis**, along which  all items will orient.

```css
.container {
	display: flex;
	align-items: center;
	/* align-items: flex-start | flex-end | center | stretch; */
}
```

### Equal Width Columns

The `.content-col` divs can be of arbitrary number, as long as they have a CSS rule that sets the `flex-basis`.

```css
/* parent div */
.container {
	display: flex;
}

/* child div */
.content-col {
	flex-basis: 100%;
}
```

### Grid-like Content Containers

This pattern will create a responsive grid without media queries. It allows rows to be of different widths. CSS Grid might not be needed in cases where this is OK.

```css
/* parent div */
.container {
	display: flex;
	flex-wrap: wrap;
}

/* child div */
.content-item {
	flex: 1 1 10rem;
}
```

### Content & Sidebar

This pattern creates a responsive content area with a content sidebar without the need for media queries. 

```css
.container {
	display: flex;
	flex-wrap: wrap;
}

.content {
	flex: 1 1 70%;
	min-width: 25ch;
}

.sidebar {
	flex: 1 1 30%;
	min-width: 15ch;
}
```
