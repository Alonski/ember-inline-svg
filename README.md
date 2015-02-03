# ember-inline-svg

Displays SVG images inline.

## Usage

```handlebars
{{inline-svg "path/to/file"}}
```

This will display the SVG found at `/public/images/path/to/file.svg` (see below on how to change this).

You can specify a class for the element like so:

```handlebars
{{inline-svg "my-svg" class="foo"}}
```

## Configuring

### SVG Paths

By default the addon expects to find your SVG images at `/public/images/`, but you can change this
by setting the `svg.paths` option in your application's Brocfile.js

```javascript
var app = new EmberApp({
  svg: {
    paths: [
      'public/images',
      'app/svgs'
    ]
  }
});
```

### Optimizing

SVGs are optimized by [svgo](https://github.com/svg/svgo) by default.

You can configure this by setting the `svg.optimize` options:

```javascript
var app = new EmberApp({
  svg: {
    optimize: {
      plugins: [
        { removeDoctype: false },
        { removeTitle: true },
        { removeDesc: true }
      ]
    }
  }
});
```

Alternatively, you can disable it completely by setting this to false:

```javascript
var app = new EmberApp({
  svg: {
    optimize: false
  }
});
```

## Troubleshooting

##### Atrociously slow build times >:[

Longer build times have two main causes:

* huge `.svg` files
* lots of `.svg` files

You can easily run into this when using SVG fonts. By default `ember-inline-svg` processes *all* `.svg` files contained in the `/public` directory. If your fonts live somewhere inside that directory, e.g. `/public/fonts`, these files will be processed, although you will never use them (as inline SVGs).

A quick and easy fix is changing the [`svg.paths` option](#svg-paths) in the configuration. Just explicitly list all directories with images that you want processed by `ember-inline-svg`.

If the longer build time is not caused by SVG fonts, but by actual SVG images that you actually need, you can [turn of the optimization](#optimization]) as a whole or individual plugins to remove or diminish another time-consuming build step.

Currently the caching does not work as expected. The bug is tracked in [issue #15](https://github.com/minutebase/ember-inline-svg/issues/15). We are positive, that fixing this bug will speed up the builds.

## Developing

### Installation

* `git clone` this repository
* `npm install`
* `bower install`

### Running

* `ember server`
* Visit your app at http://localhost:4200.

### Running Tests

* `ember test`
* `ember test --server`

### Building

* `ember build`

For more information on using ember-cli, visit [http://www.ember-cli.com/](http://www.ember-cli.com/).
