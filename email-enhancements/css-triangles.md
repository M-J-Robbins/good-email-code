---
layout: default
title: CSS Triangles
description:  A triangle shape, made with code to avoid using an image.
group: "enhancements"
order: 2.3
--- 

# CSS triangles
I originally wrote about this back in 2014 on my old site. So reposting with some small updates.

Essentially this is exactly as it sounds, a triangle shape made from CSS (or VML for Outlook).  They come up occasionally in designs and this saves using an image.

## The code
{% highlight html %}
<div style="border:2em solid transparent;border-top-color:red;border-bottom:none;display:inline-block"></div>
<!--[if mso]>
  <v:shape path="m,l1000,0 500,1000xe" style="width:64px;height:32px;" fillcolor="red" stroked="f"><o:lock selection="t"/></v:shape>
<![endif]-->
{% endhighlight %}

This code produces a small red triangle like this.
<div style="border:2em solid transparent;border-top-color:red;border-bottom:none;display:inline-block"></div>

We can make this point left, right, up or down and in in diagonal directions top left, top right, bottom right, bottom left.


## The CSS part
{% highlight html %}
<div style="border:2em solid transparent;border-top-color:red;border-bottom:none;display:inline-block"></div>
{% endhighlight %}

The concept here is, if we set borders on an element that has no height or width, then the 4 sides of the border will take the shape of 4 triangles.  We can see this if we set a different colour on each side.
<div style="border:2em solid transparent;border-top-color:red;border-right-color:green;border-bottom-color:blue;border-left-color:yellow;display:inline-block"></div>

So there are a number of ways to write the code but this is the simplest I've found.  Start by setting a transparent boarder `border:2em solid transparent` then colour one side `border-top-color:red;` and remove the space from the opposite side `border-bottom:none;` and set the element to `display:inline-block`.

To get a diagonal arrow, can either put 2 sides together, here I am using top and left
{% highlight html %}
<div style="border:2em solid transparent;border-top-color:red;border-left-color:red;display:inline-block"></div>
{% endhighlight %}
<div style="border:2em solid transparent;border-top-color:red;border-left-color:red;display:inline-block"></div>

Or you can just set the border on 2 sides
{% highlight html %}
<div style="border-top:2em solid red;border-right:2em solid transparent;display:inline-block"></div>
{% endhighlight %}
<div style="border-top:2em solid red;border-right:2em solid transparent;display:inline-block"></div>

##  The VML part
{% highlight html %}
<!--[if mso]>
  <v:shape path="m,l1000,0 500,1000xe" style="width:64px;height:32px;" fillcolor="red" stroked="f"><o:lock selection="t"/></v:shape>
<![endif]-->
{% endhighlight %}

For MSO Outlook, we have to use VML([Vector Markup Language](https://docs.microsoft.com/en-us/windows/win32/vml/web-workshop---specs---standards----introduction-to-vector-markup-language--vml-)) to get the same effect.  VML is a deprecated language used for drawing shapes, similar to SVG.  We can actually draw a number of shapes with VML I'd like to write about this more in the future but for now we'll focus on the simple triangle.

Big thanks to [Stig](https://twitter.com/stigm) who helped me out with this original code back in my 2014 article.

*Please note* to get VML to work you need to Outlook specific `xmlns:v="urn:schemas-microsoft-com:vml"` and `xmlns:o="urn:schemas-microsoft-com:office:office"` applied to your `<html>` element as described in the [email template HTMl element](https://www.goodemailcode.com/email-code/template#html-element) article.  If for some reason you can't add that to your HTML element then you can apply it directly to each `<v:shape>` element.


### `<v:shape></v:shape>`
This defines a customer shape that we're going to draw, there are also a number of predefined shapes `rect`, `roundrect`, `line`, `polyline`, `curve`, `arc`.

### `path="m,l1000,0 500,1000xe"`
The path gives the coordinates of the shape.

`m` defines the stating point of the line. Here were' not defining a position just `m,` so that will start of the default top left position `0,0`

`l` draws a line, from our start position.

`1000,0` moves the line 1000 from the left and 0 from the top.

`500,1000` sets the next point 500 from the left and 1000 from the top.

`x` returns the line back to the start point set in the `m`.

`e` stops drawing.

To help you out a bit, here are the paths for each direction;
* Down - `m,l1000,0 500,1000xe`
* Up - `m 500,0 l1000,1000 0,1000xe`
* Left - `m 0,500 l1000,0 1000,1000xe`
* Right - `m,l1000,500 0,1000xe`
* Top right - `m,l1000,0 0,1000xe`
* Top left - `m,l1000,0 1000,1000xe`
* Bottom right - `m 1000,0 l1000,1000 0,1000xe`
* Bottom left - `m,l1000,1000 0,1000xe`

### `style="width:64px;height:32px;"`
This sets the height and the width of the shape. It will stretch and distort like an `<img>` rather than fit to the size like an `<svg>`.  I've also switched the `em` to `px` here as VML seems to have issues with the size of em.

I did previously have `mso-position-horizontal:center;` set in the styles too, but found this doesn't do anything, if you want to align the shape just use `text-align` on the parent element.

### `fillcolor="red"`
Sets the colour of the shape.

### `stroked="f"`
This turns the default stroke off.  If you want to use a stroke you can add a [VML Stroke Element](https://docs.microsoft.com/en-us/windows/win32/vml/msdn-online-vml-stroke-element).

### `<o:lock selection="t"/>`
This makes the shape not selectable.  Personally I find the naming is a little confusing here, setting it to true so it's not selectable, but I believe the logic here is saying lock selection true.
