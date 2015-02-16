Parallax-Scrolling
==================
Parallax scrolling is a special scrolling technique in computer graphics, wherein background images move by the camera slower than foreground images.

### What exactly is Parallax Scrolling?
> Parallax Scrolling is the effect caused when a layer in a website moves at a different speed to another, normally activated as you scroll down but sometimes activated as you hover your cursor.

#### 1. Include and initiate Skrollr.js

> As a first step we need to include Skrollr.js  preferably before the closing body tag. This plugin will do the magic and will animate the element properties on page scroll. Skrollr is a stand-alone parallax scrolling JavaScript library for mobile (Android, iOS, etc.) and desktop. No jQuery. Just plain JavaScript.

```sh
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script>window.jQuery || document.write('<script src="js/vendor/jquery-1.9.1.min.js"><\/script>')</script>
<script src="js/skrollr.js"></script>
<script src="js/_main.js"></script>
```

Initiate the Skrollr inside of the _main.js file. You can log the current scroll position if you need to work out a precise timing and positioning of your animations.

```sh
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

Now lets have a look at the markup and Skrollr settings of the individual slides.

#### 2. Slide #1 – Fade out elements
Section height – 100% of the viewport, resized on page load

```sh
/* CSS */
.hsContainer {
    display: table;
    table-layout: fixed;
    width: 100%;
    height: 100%;
    overflow: hidden;
    position: relative;
    opacity: 0;
}
.hsContent {
    max-width: 450px;
    margin: -150px auto 0 auto;
    display: table-cell;
    vertical-align: middle;
    color: #ebebeb;
    padding: 0 8%;
    text-align: center
}
.bcg {
    background-position: center center;
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover;
    height: 100%;
    width: 100%;
}
/* Slide 1 */
#slide-1 .bcg {background-image:url('../img/bcg_slide-1.jpg')}
```

```sh
<!-- HTML -->
<section id="slide-1" class="homeSlide">
    <div class="bcg"
        data-center="background-position: 50% 0px;"
        data-top-bottom="background-position: 50% -100px;"
        data-anchor-target="#slide-1"
    >
        <div class="hsContainer">
            <div class="hsContent"
                data-center="opacity: 1"
                data-106-top="opacity: 0"
                data-anchor-target="#slide-1 h2"
            >
                <h2>Fade out elements before <br>they leave viewport</h2>
            </div>
        </div>
    </div>
</section>
```

.hsContainer and .hsContent are two nested containers helping us to center the content vertically on the page. .bcg is a container which takes up 100% width and height of each section and contains our background image.

##### Background animation
The background image of .bcg is animating from the initial position (data-center) 50% 0px to 50% -100px. This means that the background image moves up by 100px between the start of the scrolling and when the bottom of the #slide-1 hits the top of the viewport (data-top-bottom).

##### Content fading in and out
The content of the slide starts at full opacity as specified in data-center attribute and fades out to opacity: 0 when the #slide-1 h2 hits 106 pixels from the top of the viewport, where 106 is the height of our header.

#### 3. Slide #2 – Background color animation

Section height – 310px fixed height

```sh
/* CSS - Slide 2 */
#slide-2 .bcg {
    background: none;
    background-color: #010101;
    height: 310px;
    text-align: center
}
```

```sh
<!-- HTML -->
<section id="slide-2">
    <div class="bcg"
        data-0="background-color:rgb(1,27,59);"
        data-top="background-color:(0,0,0);"
        data-anchor-target="#slide-2"
    >
        <div class="hsContainer">
            <div class="hsContent">
                <h2
                    data--200-bottom="opacity: 0"
                    data-center="opacity: 1"
                    data-206-top="opacity: 1"
                    data-106-top="opacity: 0"
                    data-anchor-target="#slide-2 h2"
                >
                    Fade me in and out
                </h2>
            </div>
        </div>
    </div>
</section>
```

##### Background animation
We are simply animating the background color from dark blue to black. data-0 contains the initial background color and data-top contains the background color to which we are animating when the #slide-2 hits the top of the viewport.

##### Content fading in and out
The content fades in when #slide-2 h2 is 206 pixels from the bottom of the viewport and fades out similar way as the #slide-1 content.


#### 4. Slide #3 – Move background image horizontally

Section height – 100% of the viewport, resized on page load

```sh
/* CSS - Slide 3 */
#slide-3 .bcg {background-image:url('../img/bcg_slide-3.jpg')}
```

```sh
<!-- HTML -->
<section id="slide-3" class="homeSlide">
    <div class="bcg"
        data-center="background-position: 0px 50%;"
        data-bottom-top="background-position: 0px 40%;"
        data-top-bottom="background-position: -40px 50%;"
        data-anchor-target="#slide-3"
    >
        <div class="hsContainer">
            <div class="hsContent">
                <div class="plaxEl"
                    data-106-top="opacity: 0"
                    data-bottom="opacity: 1; position: fixed; top: 206px; width: 100%; left: 0;"
                    data--30p-top="opacity: 1;"
                    data--60p-top="opacity: 0;"
                    data-anchor-target="#slide-3"
                >
                    <h2>Fixed element fading in and out</h2>
                </div>
            </div>
        </div>
    </div>
</section>
```

##### Background animation
The background image on this slide is only slightly moving up until the slide is centered in the viewport. Then it’s moving 40 pixels left as specified in the ending position data-top-bottom="background-position: -40px 50%;".

##### Fixed content
The content is this time fixed to 206px from the top of the slide and doesn’t move. It fades in when the #slide-3 is 106 pixel from the top of the viewport and stays at full opacity until the slide is 30% above the top of the viewport. Then it fades out when 60% of the slide is out of the view.

> Note: Using the percentage instead of pixels is very handy especially if you don’t know how tall your sections will be – e.g. if you are using javascript to keep sections 100% height of your viewport on window resize.


# Conclusion

If you want to create a parallax scrolling website that works and looks great, keep these points in mind:

Less is more – avoid lots of elements flying quickly through the viewport. Subtle movements softened by fading in and out usually look the best.
Keep it natural – avoid cars animating vertically, their natural way is horizontal movement. A car coming from the side into the viewport will be less distracting than car falling down from the top.
Make it readable – try to avoid text animating over objects with the same color, it will become unreadable.
Timing is everything – make sure that your content is perfectly aligned and everything looks the best when the section is centered in the viewport. Having it messy and out of place before and after is part of the beauty of parallax scrolling websites.

Have fun – you will create an amazing things when you will enjoy playing with different settings and effect.
Keep trying – you might not get it right the first time, just keep trying and things will improve.
Let me know in the comments below what are your tricks or struggles when it comes to developing a parallax scrolling websites. I would love to hear your thoughts.
