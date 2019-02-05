![artboard](https://user-images.githubusercontent.com/659829/49244473-bd4ed580-f3c4-11e8-8bf2-498585148910.jpg)

A dead simple, zero-dependency, promise-based javascript library for extracting the dominant color(s) from an image (in the browser).

[![npm version](http://img.shields.io/npm/v/rgbaster.js.svg?style=flat)](https://npmjs.org/package/rgbaster.js "View this project on npm")


> 👉 Version 2 was written from the ground up with a clean and modern API, a robust test suite, and is fully written in Typescript.

## Installation

```
npm install --save rgbaster
```
Or download the `umd` build from the [unpkg]('https://unpkg.com/rgbaster@2.1.0/dist/rgbaster.umd.js') CDN (recommended)

You can also include it directly in a `script` tag, but you would need to load images from a server with a proper [cors]('https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_enabled_image') settings.

## Usage

This library exports a default function, or defines the global `rgbaster` function in the `umd` build, which returns a promise resolving to a sorted array with
the most dominant color at index 0, secondary at index 1, so on and so forth.

```js
[
  { color: 'rgb(0,0,255)', count: 86  },
  { color: 'rgb(9,18,42)', count: 32  },
  { color: 'rgb(120,8,202)', count: 3  },
]
```
The `npm` way:

```javascript
import analyze from 'rgbaster'

const result = await analyze('/2px-blue-and-1px-red-image.png') // also supports base64 encoded image strings

console.log(`The dominant color is ${result[0].color} with ${result[0].count} occurrence(s)`)
// => The  dominant color is rgb(0,0,255) with 2 occurrence(s)

console.log(`The secondary color is ${result[1].color} with ${result[1].count} occurrence(s)`)
// => The  secondary color is rgb(255,0,0) with 1 occurrence(s)
```
Using a `script` tag:

```javascript
const result = await rgbaster('/2px-blue-and-1px-red-image.png') // also supports base64 encoded image strings

console.log(`The dominant color is ${result[0].color} with ${result[0].count} occurrence(s)`)
// => The  dominant color is rgb(0,0,255) with 2 occurrence(s)

console.log(`The secondary color is ${result[1].color} with ${result[1].count} occurrence(s)`)
// => The  secondary color is rgb(255,0,0) with 1 occurrence(s)
```

## Configuration options

You may pass an optional second parameter, an object, with the following options:

#### `ignore`

An array of colors to ignore (in the form of `rgb`) when counting colors.

```js
const result = await analyze('/image.png', { ignore: [ 'rgb(255,255,255)', 'rgb(0,0,0)' ] })
```

#### `scale`

In order to achieve greater speed, you can have `rgbaster` scale down the image we use internally prior to analysis, thus decreasing accuracy.

```js
const result = await analyze('/image.png', { scale: 0.6 })
```
ps: the options also apply for the `script` version.

## Browser support

`rgbaster` depends on the following browser functionality:

* [Canvas](http://caniuse.com/#feat=canvas)
* [CORS](http://caniuse.com/#feat=cors)

## Maintainers

- [Alfred J. Kwack](https://github.com/AlfredJKwack)
- [Brian Gonzalez](https://github.com/briangonzalez)
- [Abdellah Hariti](https://github.com/a-hariti)

## About

`rgbaster` was created to modularize [adaptive backgrounds](http://briangonzalez.github.io/jquery.adaptive-backgrounds.js/). Check it out.

License
-------
MIT
