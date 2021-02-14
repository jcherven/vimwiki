# CSS Positioning

## Offset

The position modifier for positioning properties. Pushes an element off of the specified side of the element.

```css
.box {
	position: relative;
	top: 100px;
}
```
`top` property is the offset. This pushes .box away from the element to .box's NF top by 100px.

## Positioning Types

Defined by the `position` property. Modifies an element's position from NF.

### Static

The default positioning. The element falls into NF. Specifying an offset won't have an effect.

### NF Non-Modifying Properties

These positioning properties do not take the element out of normal flow, even if they are drawn in the browser to appear so. When these positions are applied, the NF position is still occupied by the element, even if it is visually drawn outside of its NF position.

#### Relative

Positioning context: NF

*Does not* modify the NF of the element. 

Element is drawn in a position relative to its own position *in Normal Flow*. It's not actually shifted, only drawn on the screen so that it appears so.

```css
.box {
	position: relative;
	top: 100px;
}
```

If box is in the top right corner of the page in NF, giving it a relative position and a top property will draw it shifted down from the center.

```css
.box {
	position: relative;
	top: 100px;
	right: -100px;
}
```

If the same box has a right property of a negative number added, it would be drawn as shifted to the right. With a positive value, the right property would push off of the right side of the element, but with a negative value it's semantically consistent.

```css
.box {
	position: relative;
	top: 500px;
	left: -500px;
}
```

### NF Modifying Properties

Removes an element from NF. The document will reflow. Question: will other elements now flow around this repositioned element?

#### Absolute

Modifies the NF of the element. Elements with the absolute property do not leave a reserved space in NF. The rest of the document will reflow.

Positioning context: parent (containing) element

Element is drawn in a position relative to its parent (containing) element in NF.

```css
.parent {
	position: relative;
}
.box {
	position: absolute;
	top: 100px;
}
```

Assume .box is nested inside .parent in the markup. .box will be drawn such that its top is pushed off 100px .parent's top.

```css
.parent {
	position: relative;
}
.box {
	position: absolute;
	bottom: 0px;
	right: 0px;
}
```

this would stick .box in the bottom right corner of .parent.

```css
.parent {
	position: relative;
}
.box {
	position: absolute;
	bottom: 0px;
	left: -200px;
}
```

This would stick .box's bottom against .parent's bottom, and shift .box outside of .parent's left.

#### Fixed

Positioning context: the browser window (viewport)

Fixed elements use the offset value that relative and absolute use. Fixed elements don't always appear to be semantically moved in the direction that their properties state. The offset behavior applies.

Fixed elements will stay in position when the browser is resized; the term "fixed" refers to its relativity to the browser viewport.

```css
.box {
	position: fixed;
	top: 100px;
	right: 100px;
}
```

This would position .box pushed down from the viewport's top and pushed off of the viewport's right.

```css
.box {
	position: fixed;
	top: 0px;
	right: 0px;
}
```
This positions .box directly in the bottom right corner of the viewport.

#### Sticky

Positioning context: the containing element under certain conditions

A sticky element behaves as relative until the element is scrolled up to its parent. At this point, the element behaves as fixed.

```css
.box {
	position: sticky;
	top: 0px;
}
```

## Z-Index
