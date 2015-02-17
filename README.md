#Working on it

Parallax-Scrolling
==================
Parallax scrolling is a special scrolling technique in computer graphics, wherein background images move by the camera slower than foreground images.

### What exactly is Parallax Scrolling?
> Parallax Scrolling is the effect caused when a layer in a website moves at a different speed to another, normally activated as you scroll down but sometimes activated as you hover your cursor.

### Abstract
> skrollr allows you to animate any CSS property of any element. All you need to do is define key frames for each element at certain points in top scroll offset.

#### 1. Include and initiate Skrollr.js

> As a first step we need to include Skrollr.js  preferably before the closing body tag. This plugin will do the magic and will animate the element properties on page scroll. Skrollr is a stand-alone parallax scrolling JavaScript library for mobile (Android, iOS, etc.) and desktop. No jQuery. Just plain JavaScript.

```html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script>window.jQuery || document.write('<script src="js/vendor/jquery-1.9.1.min.js"><\/script>')</script>
<script src="js/skrollr.js"></script>
<script src="js/_main.js"></script>
```

Initiate the Skrollr inside of the _main.js file. You can log the current scroll position if you need to work out a precise timing and positioning of your animations.

```html
( function( $ ) {
    // Init Skrollr
    var s = skrollr.init({
        render: function(data) {
            //Debugging - Log the current scroll position.
            //console.log(data.curTop);
        }
    });
} )( jQuery );
```
#### Or

```html
var s = skrollr.init();
```
Now lets have a look at the markup and Skrollr settings of the individual slides.

### Lets get the basics of view, How skrollr.js works.
Here's an infographic for better understanding of anchors (click to open PDF):

[![Anchors Guide](https://raw.githubusercontent.com/ajaykumaryadav/Parallax-Scrolling/master/guide/anchor-position-guide.png)](https://raw.githubusercontent.com/ajaykumaryadav/Parallax-Scrolling/master/guide/anchor-position-guide.pdf)

### Absolute vs relative mode

Being only able to define key frames in absolute values is simply insufficient for some cases. For example, if you don't know exactly where an element will be in the document. That's why there are two modes for key frames, namely absolute and relative mode.

#### Absolute mode (or document mode)
The key frames are defined as absolute values describing how much the **document** has been scrolled down.

The syntax is `data-[offset]-[anchor]`, where `offset` can be any integer (0 is default) and `anchor` can be either `start` (default) or `end`. Either `offset` or `anchor` can be omitted in some situations. Here are some examples of key frames and their meaning.

* `data-0` = `data-start` = `data-0-start`: When the scroll top is 0.
* `data-100` = `data-100-start`: When the scroll top is 100.
* `data--100` = `data--100-start`: When the scroll top is -100 (sounds like nonsense, but keep in mind that interpolation will be relative to this point).
* `data-end` = `data-0-end`: When offset is 0, but counting from the bottom of the document instead of from the top. In short: when you reach the bottom of the page.
* `data-100-end`: 100px before we reach the bottom.
* `data--100-end`: 100px after we reach the bottom (again, it's up to you whether you need it).


### Relative mode (or viewport mode)

Instead of defining key frames relative to the **document** (i.e. absolute), we are able to define them depending on the position of any element in relation to the **viewport**.

The syntax is `data-[offset]-(viewport-anchor)-[element-anchor]`, where `offset` can again be any integer and defaults to 0. Both `viewport-anchor` (mandatory) and `element-anchor` (optional) can be one of `top`, `center` or `bottom`. If `element-anchor` is omitted, the value of `viewport-anchor` will be taken (just like with background-position). Here are some examples of key frames and their meaning.

* `data-top` = `data-0-top` = `data-top-top` = `data-0-top-top`: When the element's top is aligned with the top of the viewport.
* `data-100-top` = `data-100-top-top`: When the element's top is 100px above the top of the viewport.
* `data--100-top` = `data--100-top-top`: When the element's top is 100px below the top of the viewport.
* `data-top-bottom `= `data-0-top-bottom`: When the bottom of the element is at the top of the viewport (it's just not visible).
* `data-center-center` = `data-0-center-center`: When the element is at the center of the viewport.
* `data-bottom-center` = `data-0-bottom-center`: When the element's center is at the bottom of the viewport, thus the upper half of the element is visible.

By default the keyframes are triggered by the position of the element where the keyframes are described.  However there are times when the position of a second element should trigger the first element's keyframes.  The  `data-anchor-target` attribute can be used in these cases.  The `data-anchor-target` attribute accepts any CSS selector and the position of the first element on the page matching the selector will be used to trigger keyframes on the element where the attribute is defined. `data-anchor-target` requires IE 8 or greater.

Examples: `<div `data-anchor-target="#foo"`>`  will have it's keyframes tiggered by  the position of the `#foo element`.  Any CSS selector can be used, i.e  `data-anchor-target=".bar:not(.bacon) ~ span > a[href]"`

**Note**: If you need to support IE 7, then you may only use IDs as `anchor-target`s, i.e. `#foo`. The IE plugin maps `querySelector` to `getElementById`.

**Important**: All those values will be calculated up-front and transformed to `absolute` mode. So if either the element's box height changes (height, padding, border) or the elements position within the document, you probably need to call `refresh()` (see documentation in JavaScript section below). **Window resizing is handled by skrollr.**


Limitations
-----

There are some limitations of skrollr you should be aware of.

* All numeric values have to have the same unit, even `0` needs a unit. It's not possible to animate from `5%` to `100px`. skrollr won't complain, but results are undefined.
* Animations between values which are composed of multiple numeric values like `margin:0 0 0 0;` are only possible for the same number of values. `margin:0px 0px 0px 0px;` to `margin:0px 100px 50px 3px;` is fine, but not `margin:10px;` to `margin:5px 10px;`.
* Animations between CSS transforms only work when they use the same functions in same order. From `rotate(0deg) scale(1)` to `rotate(1000deg) scale(5)` is fine.
* Color animations don't support named values like "red" or hex values like "#ff0000". Instead, you have to use `rgb()`, `rgba()`, `hsl()` and `hsla()`. Don't worry, there's a skrollr plugin for IE < 9 to support `hsl()` (without "a"!) and to fall rgba back to rgb.
* Color animations only work for same color functions. `hsl()` to `hsl()` or `hsla()` is fine, but not `rgb()` to `hsl()`. Which makes sense, because animating from the same colors in rgb space and in hsl space results in different animations (hsl gives you the nice rainbow stuff).
