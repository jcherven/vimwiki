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
	<a class="recipe__btn">
	</a>
</figure>
```

### Modifier

A Modifier is a different version of an element. Here we modify the `btn` class with `--round`.

```html
<figure class="recipe">
	<a class="recipe__btn btn btn--round">
	</a>
</figure>
```

Rather than using a specific selector like `btn.round`, a more general selector can be used to select `btn`s that need to be round.

## 7-1 Architecture

7-1 can be used to organize style code for preprocessors like Sass. It organizes source files into 7 different folders for partial Sass files, and one main Sass file which imports all of these. The preprocessor will compile these to one sylesheet for client rendering in a build step.

```
7 Folder Tree

projectRoot
└── Sass
		├── abstracts (variables, functions, mixins)
		├── base
		├── components
		├── layout
		├── pages (specific page styles)
		├── themes
		└── vendors

```

Not all of the folders need to be used in every project.
