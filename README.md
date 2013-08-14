# Horizontal packing

Packs images into rows so that each row takes up the full width.
Row heights are dynamically adjusted.
Similar to Masonry, but the space taken by all the grids will always be a rectangle versus any jagged edge.
By being horizontal, it is also more linear (scan left to right, top to bottom).

Demo: http://jonathanong.github.io/hor-pack/

See:

- https://github.com/jonathanong/linear-partition
- https://news.ycombinator.com/item?id=6198400
- http://www.crispymtn.com/stories/the-algorithm-for-a-perfectly-balanced-photo-gallery

## Install

```bash
bower install jonathanong/hor-pack
```

or

```bash
component install jonathanong/hor-pack
```

## API

### Layout

The HTML must strictly be a single container whose children are strictly grid elements.

```html
<div>
  <img data-width="100" data-height="320">
  <div data-aspect-ratio=".55"></div>
  <element></element>
  <element></element>
</div>
```

This library assumes you know the aspect ratio of each grid element.
Each element should either have a `data-aspect-ratio` attribute, `data-width` and `data-height` attributes, or a `.aspectRatio` attribute.
If you do not know these attributes, use a library such as [imagesloaded](https://github.com/desandro/imagesloaded) to calculate the dimensions before using this library.

### Pack(container, options)

Returns a new instance of `Pack`.

```js
var pack = new Pack(container, options)
```

`new` is optional.
`container` is the element that contains all the grids.
The `options` are:

- `height` - Target row height.
  `Math.round(window.innerHeight / 3)` by default.
- `padding` - Padding between each grid.
  `0` by default.

Each of these options can be changed as an attribute of `pack`:

```js
// Change the target height
pack.height = Math.round(window.innerHeight / 5)
// Change the padding
pack.padding = 5
// Recalculate the grid
pack.reload()
```

Other options you may be interested are:

- `width` - the width of the grid.
  You should change this when `container`'s width changes.

### pack.reload()

Recalculates the grid.
Specifically, you would want to use this when the image is resized:

```js
window.addEventListener('resize', function () {
  pack.width = container.clientWidth
  pack.height = Math.round(window.innerHeight / 3)
  pack.reload()
})
```

Note: you may want to debounce this function if you care about performance.

### pack.destroy()

Destroys the grid.

### pack.create()

Creates the grid.
This is called by default.
You should only use this if the grid has been previously destroyed.

### pack.append(elements)

Append elements to the current grid.

## Compatibility

IE9+ due to the use of ES5 Array methods.

## License

The MIT License (MIT)

Copyright (c) 2013 Jonathan Ong me@jongleberry.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.