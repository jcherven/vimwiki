# Sass Preprocessor

## Variables

### Define a variable:

```scss
$color-primary: #f9ed69;
```

### Reference a variable:

```scss
nav {
	background-color: $color-primary;
}
```

## Nesting Rules (Nested Selectors)

Pure CSS method of specific child selectors:

```css
.navigation li {}
```

Nested Selectors with Sass:

```scss
.navigation {
	list-syle: none;
	li{
		display: inline-block;
	}
	li:first-child {
		margin: 0;
	}
}
```

The Sass preprocessor will compile this nested rule to `.navigation li {}`

#### Repeating nesting with the ampersand operator

An `&` operator can replace the parent selector path to enable deep nesting.

```scss
.navigation {
	list-syle: none;
	li { /* compiles to `.navigation li` outside of this block */
		display: inline-block;
		
		&:first-child { /* compiles to `.navigation li:first-child` outside of this block*/
			margin: 0;
		}
		
		a { /* compiles to `.navigation li a` outside of this block */
			text-decoration: none; 
			text-transform: uppercase;
		}
	}
}
```

## Functions

Sass has built-in functions as well as the ability to use custom functions.

```css
btn:hover {
	background-color: lighten($color-secondary, 10%);
}
```

### Custom Functions

```scss
@function divide($a, $b) {
	@return $a / $b;
}

nav {
	margin: divide(60, 2) * 1px; // compiles to a value returned of 30px
}

```

## Mixins

Mixins are re-usable rule blocks referenced by an identifier, similar to macros.

```scss
@mixin clearfix {
	&::after {
		content: "";
		clear: both;
		display: table;
	}
}
```

This can be used in another part of the stylesheet as a rule with the `@inlcude` statement:

```scss
@include clearfix;
```

Mixins are commonly used to turn groups of similar declarations into DRY-conformant code. In this circumstance, the mixin is used as a declaration. It might be preferrable to use Extends for declarations instead. TODO

```scss
@mixin style-link-text {
	text-decoration: none;
	text-transform: uppercase;
	color: $color-text-light;
}

.btn-hot:link {
	padding: 10px;
	display: inline-block;
	@include style-link-text;
}
```

### Mixin declarations with args

Define a mixin with one or more parameters to use different values.

```scss
@mixin style-link-text($color) {
	text-decoration: none;
	text-transform: uppercase;
	color: $color;
}

.btn-hot:link {
	padding: 10px;
	display: inline-block;
	@include style-link-text($color-text-dark);
}
```
## Extends

Extends are partial blocks of CSS declarations. Define an extend with the `%` operator. It might be preferrable to use mixins for rules and extends for declarations. TODO

```scss
%btn-placeholder {
	padding: 10px;
	display: inline-block;
	text-align: center;
	border-radius: 100px;
	width: $width-button;
	@include style-link-text($color-text-light);
}
```

The extend can then be used as a partial block of declarations.

```scss
.btn-main {
	&:link {
		extend %btn-placeholder;
		background-color: $color-secondary;
	}
}
```
