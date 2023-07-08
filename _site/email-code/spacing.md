<div class="updated">Last Updated: <time datetime="2022-03-01">1<sup>st</sup> March 2022</time></div>


# Spacing
Spacing seems like a very simple task but to do it accurately in email can get a little tricky at times.

Your first options should always be using `margin` or `padding`, [support for margin](https://www.caniemail.com/features/css-margin/) and [support for padding](https://www.caniemail.com/features/css-padding) is pretty good across emails clients with a few small issues in Outlook.

If you are still having issue then you can try these methods.

## Horizontal Spacer

### The Code
```html
<i style="letter-spacing:50px;mso-font-width:-100%;display:inline-block;width:50px">&#8202;</i>
```

To get it working in MSO Outlooks we are using `letter-spacing` to create the size of this spacer. And for `letter-spacing` to work we need a letter for it to work off.  In this case we are using a _"Hair Space"_ `&#8202;`.  This is the thinest character I found so it only adds a very tiny amount of space onto the 50px specified in the `letter-spacing`.  To remove that spacing from MSO Outlooks we can use `mso-font-width:-100%;`

For HTML email clients we can add `display:inline-block;width:50px`.


## Vertical Spacer

### The Code
```html
<div style="line-height:50px; height:50px;">&#8202;</div>
```

Again we need to insert a character, this time to have something for the `line-height` to respond to and stop the `<div>` from collapsing, I've used `&#8202;` again for consistency with the horizontal spacer, but other characters should work too.  Gmail app on Android adds a little extra space here so setting a fixed `height` the same as the `line-height` brings that in line.

**N.B** If the `line-height` is less than the current `font-size`, then you'll also need to add a `font-size` 

```html
<div style="line-height:8px; height:8px; font-size:8px">&#8202;</div>
```

## Horizontal & Vertical Spacer

## The Code
```html
<i style="letter-spacing:50px;mso-font-width:-100%;display:inline-block;width:50px;
font-size:0px;mso-text-raise:50px;height:50px;">&#8202;</i>
```

This is mostly the same as the horizontal spacer but we're adding `mso-text-raise` to set the hight for Outlook, and using `font-size:0px` to remove the additional hight we would get from having the `&#8202;`.  And using `height` for all the HTML email clients.
