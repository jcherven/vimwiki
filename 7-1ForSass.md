# 7-1 Architecture for Sass

- `abstracts` should contain code abstractions like variables, functions, mixins, and extends.
- `base` should contain basic visual components like:
	- site-wide tags like `<html>` and `<body>`

In the project root folder, run:

```bash
mkdir -p sass/{abstracts,base,components,layout,pages,themes,vendors}
touch sass/main.scss
touch sass/base/{_base.scss,_animations.scss,_typography.scss,_utilities.scss}
touch sass/abstracts/{_variables.scss,_mixins.scss,_functions.scss}
```

The project tree should resemble this:

```
projectRoot/
├── sass/
│		├── abstracts/
│		│   ├── _functions.scss
│		│   ├── _mixins.scss
│		│   └── _variables.scss
│		├── base/
│		│   ├── _animations.scss
│		│   ├── _base.scss
│		│   ├── _typography.scss
│		│   └── _utilities.scss
│		├── components/
│		│   └── _button.scss
│		├── layout/
│		│   └── _header.scss
│		├── pages/
│		│   └── _home.scss
│		├── themes/
│		├── vendors/
│		└── main.scss
└── index.html
```


