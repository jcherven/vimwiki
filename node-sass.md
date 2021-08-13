# The node-sass package

## Creating a preprocessor build script for Nodejs

This example presupposes a `main.scss` file in a 7-1 `sass` directory with a `projectRoot/css/style.css` file that is referenced by `index.html`.

The `npm run` command provides the `-w` flag to watch a source file for saved changes.

`projectRoot/package.json`
```json
{
	...
	"scripts": {
		"compile:sass": "node-sass <input file> <output file> -w"
	}
	...
}
```

## Example Sass dev and build pipeline with Nodejs

```json
...
"scripts": {
	"watch:sass": "node-sass sass/main.scss css/style.css -w",
	"devserver": "lite-server",
	"start": "npm-run-all --parallel devserver watch:sass",
	"compile:sass": "node-sass sass/main.scss css/style.comp.css",
	"prefix:css": "postcss --use autoprefixer -b 'last 10 versions' css/style.comp.css -o css/style.prefix.css",
	"compress:css": "node-sass css/style.prefix.css css/style.css --output-style compressed",
	"build:css": "npm-run-all compile:sass prefix:css compress:css"
},
"devDependencies": {
	"autoprefixer": "^7.2.6",
	"concat": "^1.0.3",
	"lite-server": "^2.6.1",
	"node-sass": "^6.0.1",
	"npm-run-all": "^4.1.5",
	"postcss-cli": "^8.3.1"
},
...
```
