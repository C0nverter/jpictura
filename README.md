﻿# jPictura

jPictura is a simple jQuery plugin for alignment of images.

## Table of contents

* [Quick start](#quick-start)
* [Options](#options)

## Quick start

### Installation

* Install with [npm](https://www.npmjs.com): `npm install jpictura`.

The following two files have to be used in your solution:

```
jpictura/
└── dist/
    ├── css/
    │   └── jpictura.min.css
    └── jpictura.min.js
```

### Setup

Include ```jpictura.min.css``` inside of your head tag and ```jpictura.min.js``` just before the closing body tag. Be sure to include jQuery before jpictura.min.js.

```html
<head>
    <title>Your Intergalactic Website</title>        
    <link rel="stylesheet" href="jpictura/dist/css/jpictura.min.css">
</head>
<body>
        
    <script src="http://code.jquery.com/jquery-2.2.0.min.js"></script>
    <script src="jpictura/dist/jpictura.min.js"></script>
</body>
```

Create a target gallery element with divs inside, one for each image. Skippr targets div tags with class ```item``` (can be changed in the options [](#options)) inside of the selected element.

```html
<div id="my-gallery">
    <div class="item"><img src="foo.png" /></div>
    <div class="item"><img src="bar.png" /></div>
</div>
```

### Initialization

Simply select the gallery element and call the ```jpictura``` method. It is that simple!

```javascript
$(document).ready(function(){
    $("#my-gallery").jpictura();
});
```

## Options

Customize your gallery by passing an options object as a single parameter to the ```jpictura``` method.

```javascript
$(document).ready(function(){
    $("#my-gallery").jpictura({ itemSpacing: 5, justifyLastRow: false });
});
```

The complete options object looks like this:

```javascript
var options = {
    selectors: {
        item: '.item',
        image: 'img'
    },
    classes: {
        container: 'jpictura',
        item: 'jpictura-item',
        image: 'jpictura-image',
        lastRow: 'jpictura-last-row',
        firstInRow: 'jpictura-first-in-row',
        lastInRow: 'jpictura-last-in-row'
    },
    layout: {
        rowPadding: 0,
        itemSpacing: 0,
        applyItemSpacing: true,
        idealRowHeight: 180,
        minWidthHeightRatio: 1 / 3,
        maxWidthHeightRatio: 3,
        stretchImages: true,
        allowCropping: true,
        croppingEpsilon: 3,
        centerImages: true,
        justifyLastRow: false
    },
    effects: {
        fadeInItems: false
    },
    waitForImages: true,
    heightCalculator: heightCalculator,
    algorithm: {
        epsilon: 0.01,
        maxIterationCount: 100
    },
    debug: false
};
```

The options are described in details in the following sections.

### selectors.item

A jQuery selector that is used to locate the gallery items within the container.

#### Example

```html
<div id="my-gallery">
    <a href=""><img src="foo.png" /></a>
    <a href=""><img src="bar.png" /></a>
</div>

$(document).ready(function(){
    $("#my-gallery").jpictura({ selectors: { item: 'a' } });
});
```

### selectors.image

A jQuery selector that is used to locate the images within the gallery items.

#### Example

```html
<div id="my-gallery">
    <div class="item"><img src="ANOTHER IMAGE" /><img class="chosen-image" src="foo.png" /></div>
    <div class="item"><img src="ANOTHER IMAGE" /><img class="chosen-image" src="bar.png" /></div>
</div>

$(document).ready(function(){
    $("#my-gallery").jpictura({ selectors: { image: '.chosen-image' } });
});
```

### classes

CSS classes that are automatically applied by the plugin to specific elements.

:warning: The CSS classes are used internally by the plugin's CSS. Chaning one of them may cause the plugin to misbehave.