# gulp-twig

Uses [twig.js](https://www.npmjs.com/package/twigjs) to compile Twig templates.

## Usage

First, install `gulp-twig` as a development dependency:

```shell
npm install --save-dev gulp-twig@git+https://git@github.com/backflip/gulp-twig.git
```

Then, add it to your `gulpfile.js`:

```javascript
var twig = require('gulp-twig'),
    path = require('path'),
    rename = require('gulp-rename');

gulp.task('html', function(){
  gulp.src(['./source/*.twig'])
    .pipe(twig({
        data: {
            title: 'hello'
        },
        includes: [
            './source/layouts/*.twig',
            './source/includes/*.twig'
        ],
        getIncludeId: function(filePath) {
            return path.relative('./source', filePath);
        }
    }))
    .pipe(rename({
        extname: '.html'
    }))
    .pipe(gulp.dest('./build/'));
});
```

## Options

### options.data
Type: `Object|Function`

An object of data to pass to the compiler. If of type `function`, the Vinyl file object is passed as argument:
```js
data: function(file) {
    return file.data;
}
```

### options.includes
Type: `String|Array`

Single or array of globs of includes to be registered.

### options.getIncludeId
Type: `Function`

Transformation function for template ID. If omitted, the file path is used. In the example above, `source/layouts/layout.twig` would be registered as `layout/layout.twig`.
