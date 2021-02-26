# npm-build-boilerplate
This boilerplate is all about using npm scripts as a build tool

## Used packages
* `postcss-cli` to run `autoprefixer`
* `browser-sync` development server
* `eslint` to lint JavaScript using `standard` style guide
* `imagemin-cli` to minify images
* `npm-run-all` to run multiple npm scripts
* `onchange` to watch file sets and run commands when anything changes
* `sass` preprocessor
* `stylelint` CSS linter with `stylelint-config-standard` styleguides and `stylelint-scss` plugin for SCSS specific rules
* `svg-sprite-generator` SVG sprite file generator
* `svgo` SVG optimizer
* `uglify-js` JavaScript minifier, compressor and beautifier toolkit

## Tasks list
### `postinstall`
`npm run start`

### `build`
`run-s build:*`

### `build:css`
`npm run lint:scss && npm run scss && npm run prefixer`

### `build:html`
`cp index.html dist`

### `build:img`
`npm run imagemin && npm run svg`

### `build:js`
`npm run lint && npm run uglify`

### `clean`
`rimraf dist`

### `imagemin`
`imagemin src/img/*.{jpg,JPG,jpeg,png,PNG,gif,GIF,webp} --out-dir=dist/img`

### `lint`
`eslint src/js`

### `lint:scss`
`stylelint src/scss/**/*.scss --syntax scss`

### `prefixer`
`postcss dist/css/*.css -u autoprefixer --autoprefixer.browsers 'last 5 versions' -r`

### `sass-update`
`sass --update src/scss:dist/css`

### `sass-watch`
`sass --watch --style=compressed src/scss:dist/css`

### `scss`
`sass --no-source-map --style=compressed src/scss/style.scss dist/css/style.min.css`

### `serve`
`browser-sync start -s dist -f 'dist/**/*' --port 9000 --no-inject-changes`

### `start`
`run-s clean build watch`

### `svg`
`svgo -f src/img -o dist/img && svg-sprite-generate -d dist/img -o dist/img/sprite.svg`

### `uglify`
`npx mkdirp dist/js && uglifyjs src/js/*.js -m -b -o dist/js/app.js && uglifyjs src/js/*.js -m -c -o dist/js/app.min.js`

### `watch`
`run-p serve watch:*`

### `watch:css`
`onchange src/scss/*.scss -- npm run build:css`

### `watch:html`
`onchange index.html -- npm run build:html`

### `watch:img`
`onchange src/img/**/* -- npm run build:img`

### `watch:js`
`onchange src/js/*.js -- npm run build:js`
