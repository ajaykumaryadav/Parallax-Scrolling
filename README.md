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
### Or

```html
var s = skrollr.init();
```
Now lets have a look at the markup and Skrollr settings of the individual slides.

[![Anchors Guide](#)](#)