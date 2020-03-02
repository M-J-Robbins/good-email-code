# CSS triangles
I originally wrote about this back in 2014 on my old site. So reposting with some small updates.

Essentially this is exactly as it sounds, a triangle shape made from CSS.
## The code
{% highlight html %}
<div style="border:2em solid transparent;border-top-color:red;border-bottom:none;display:inline-block"></div>
<!--[if mso]>
  <v:shape path="m,l1000,0 500,1000xe" style="width:64px;height:32px;mso-position-horizontal:center;" fillcolor="red" stroked="f"><o:lock selection="t"/></v:shape>
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
  <v:shape path="m,l1000,0 500,1000xe" style="width:64px;height:32px;mso-position-horizontal:center;" fillcolor="red" stroked="f"><o:lock selection="t"/></v:shape>
<![endif]-->
{% endhighlight %}

For MSO Outlook, we have to use VML([Vector Markup Language](https://docs.microsoft.com/en-us/windows/win32/vml/web-workshop---specs---standards----introduction-to-vector-markup-language--vml-)) to get the same effect.  VML is a deprecated language used for drawing shapes, similar to SVG.  We can actually draw a number of shapes with VML I'd like to write about this more in the future but for now we'll focus on the simple triangle.


Big thanks to Stig who helped me out with this original code back in 2014.

### `<v:shape></v:shape>`
This defines a customer shape that we're going to draw, there are also a number of predefined shapes `rect`, `roundrect`, `line`, `polyline`, `curve`, `arc`.

### `path="m,l1000,0 500,1000xe"`
The path gives the coordinates of the shape. `m` defines the stating point of the line. Here were' not defining a position just `m,` so that will start of the default top left position `0,0`
`l` draws a line, from our start position.
`1000,0` moves the line 1000 from the left and 0 from the top.
`500,1000` sets the next point 500 from the left and 1000 from the top.
`x` returns the line back to the start point set in the `m`.
`e` stops drawing.

### `style="width:64px;height:32px;mso-position-horizontal:center;"`

### `fillcolor="red"`

### `stroked="f"`

### `<o:lock selection="t"/>`
