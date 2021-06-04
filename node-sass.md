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

