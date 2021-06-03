# BEM and 7-1 Architecture

## BEM (Block-Element-Modifier)

With Block Element Modifier architecture, rendering performance is improved by reducing specificity of CSS rules in the cascade. Since high-specificity CSS selectors negatively affect CSS rendering performance, BEM is sort of an ugly hack to make the browser treat hierarchical selectors as the most generalized selector possible, reducing specificity.

### Block

A Block is a standalone component that is meaningful on its own. A Block is identified by a class name.

```html
<figure class="recipe">
</figure>
```

### Element

An element is a part of a block that has no standalone meaning. It is appended to a Block to provide semantic specificity for reading and organizing code, but the rendering specificity is reduced to improve pageload performance.

Here, the element `__info` is appended to a `recipe` child element as a class. In the cascade, this has less specificity than a CSS selector like `.recipe.info`.

```html
<figure class="recipe">
	<div class="recipe__info">
	</div>
</figure>
```
