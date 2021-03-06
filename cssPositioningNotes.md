# CSS Positioning

## Offset

The position modifier for positioning properties. Pushes an element off of the specified side of the element.

```css
.box {
	position: relative;
	top: 100px;
}
```
`top` property is the offset for the `position` property. This pushes `.box` away from the element to `.box`'s NF top by 100px.

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

If `.box` is in the top right corner of the page in NF, giving it a relative position and a top property will draw it shifted down from the center.

```css
.box {
	position: relative;
	top: 100px;
	right: -100px;
}
```

If the same `.box` has a right property of a negative number added, it would be drawn as shifted to the right. With a positive value, the right property would push off of the right side of the element, but with a negative value it's semantically consistent.

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

Positioning context: parent (containing) element

Modifies the NF of the element. Elements with the absolute property do not leave a reserved space in NF. The rest of the document will reflow.

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

Assume `.box` is nested inside `.parent` in the markup. `.box` will be drawn such that its top is pushed off 100px from `.parent`'s top.

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

this would stick `.box` in the bottom right corner of `.parent`.

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

This would stick `.box`'s bottom against `.parent`'s bottom, and shift `.box` outside of `.parent`'s left.

#### Fixed

Positioning context: the browser window (viewport)

Fixed elements use the offset value that relative and absolute use. Fixed elements don't always appear to be semantically moved in the direction that their properties state. The offset behavior applies.

If the browser window gets resized, a fixed element will move relative to it. the term "fixed" refers to its relativity to the browser viewport.

```css
.box {
	position: fixed;
	top: 100px;
	right: 100px;
}
```

This would position `.box` pushed down from the viewport's top and pushed off of the viewport's right.

```css
.box {
	position: fixed;
	top: 0px;
	right: 0px;
}
```
This positions `.box` directly in the bottom right corner of the viewport.

#### Sticky

Positioning context: the containing element under certain conditions

A sticky element behaves as relative until the element is scrolled up to its parent. At this point, the element behaves as fixed.

```css
.box {
	position: sticky;
	top: 0px;
}
```

Here, `.box`'s top is shifted to its parent element's top. If scrolling down causes `.box`'s top to reach the viewport's top, it becomes fixed as scrolling continues.

## Float and Clear

Floats, by default, reflow the page as the floated element is taken out of NF.

Imagining the viewport as an aquarium into which the user is looking down, we can imagine block elements sinking to the bottom by default, all lining up from north to south. If the northernmost element is floated left, it rises towards the surface and to the left side of the page, and the remaining line of sunken elements slide north to fill the space. This gives the appearance of the second element disappearing, but it has in fact slid north underneath the floated element. Floated elements are removed from NF into what is apparently a secondary flow space layered on top of the viewport, and the base layer is reflowed.

If a second element is floated with `float: left;`, that element floats and flows with the previously floated element as if it were inline, displaying to the right side of the previously floated element. The base layer again reflows underneath.

In order to keep other floated elements from flowing next to each other, the `clear: left|right|both;` is used on the floated element.

Since float and clear seems to break a very important convention of NF, it's probably best to avoid using it in new projects.

## Z-Index

Higher index values are on top of lower index values. Be sure to leave numerical space between values incase you need to add something in between later.

Used like so:

```css
.blue {
	z-index: 20;
}
.green {
	z-index: 30;
}
.red {
	z-index: 10;
}
```

`.green` is on top of `.blue`, and `.red` is beneath that.
