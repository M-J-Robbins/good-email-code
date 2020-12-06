# SVG to VML
From my extensive research ([this wikipedia post](https://en.wikipedia.org/wiki/Vector_Markup_Language)) the SVG specification is, in part, based off the VML spec.  When comparing the two formats, there are a lot of similarities so I've written up this brief guide to help you manually convert SVG to VML.

## Wrapper
Both formats can have an outer wrapper, however the VML wrapper is optional. If you're only inserting a single VML element you can do it without a wrapper.

**SVG**
{% highlight html %}
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1000 500" style="width:1000px;height:500px" role="img" aria-label="alt text">
</svg>
{% endhighlight %}

**VML**
{% highlight html %}
<v:group xmlns:v="urn:schemas-microsoft-com:vml" coordsize="1000 500" style="width:1000px;height:500px" alt="alt text">
</v:group>
{% endhighlight %}

### Xmlns
This specifies the xml namespace for a document. This is optional in both cases but for VML if it's not on the shape, then it must be added to the HTML tag  `<html xmlns:v="urn:schemas-microsoft-com:vml">`

### Viewport size
Because these are vector images, they can be scaled to any size, so we need to define the dimensions of the space we're working in. Think of it like the artboard size or canvas size.  So if we place something 10 from the top and 10 from the left, it'll be relevant to the sizes we define here.

**SVG viewBox:** The SVG `viewbox` has 4 values min-x, min-y, width and height, for now we'll ignore the first 2 and assume they are both set to `0`.
**VML coordsize:** VML `coordsize` only has 2 values width and height, so these should match the last 2 values of the `viewbox`.

I need to read more into it but `coordorigin` may be comparable to the first 2 values for `viewbox`.

### Image size
We can set the actual size of our image with `width` and `height` in the `style` attribute.  This works the same in both formats `style="width:1000px;height:500px"`.

### alt text
SVG has a couple of options for alt text, we can use `<title>alt text</title>` inside the `<svg>` wrapper.  Or we can use `role="img"` to define this as an image and `aria-label="alt text"` for the alt text.

VML will converted to an `<img>` when it's displayed in Outlook, so we can simply use `alt="alt text"` here.

## Line
**SVG**
{% highlight html %}
<line x1="10" y1="20" x2="100" y2="200" stroke="#ff0000" stroke-width="2"/>
{% endhighlight %}

**VML**
{% highlight html %}
<v:line from="10,20" to="100,200" strokecolor="#ff0000" strokeweight="2pt"/>
{% endhighlight %}

### Line size
The line size and colour are done as a stroke in both SVG and VML.  SVG uses `stroke-width` VML uses `strokeweight`, with VML we need to specify a unit on the `strokeweight` so I've also added `pt` however this is not a relative unit so may need adjusting if the shape size is changed.

### Line colour
The colour of the line is set as `stroke` in SVG, with VML it's expanded a little to `strokecolor`.

### Line position
SVG starts the line with `x1` and `y1` to define the start point from the left and top and ends the line with `x2` and `y2` to define the start point from the left and top.

VML combines the X and Y coordinates, so we set 2 values in `from` (X then Y) and 2 values in `to` (X then Y).


## Square
**SVG**
{% highlight html %}
<rect />
{% endhighlight %}

**VML**
{% highlight html %}
<v:rect />
{% endhighlight %}
### Square size
### Square rounded corners
### Square position



## Circle
**SVG**
{% highlight html %}
<ellipse rx="90" ry="110.5" cx="251" cy="167.5" fill="#a8b3dc"/>
{% endhighlight %}

**VML**
{% highlight html %}
<v:oval style="width:180;height:221;position: absolute;left:161;top:57" fillcolor="#a8b3dc" stroked="f"/>
{% endhighlight %}

### Circle element
SVG has 2 options `<circle />` or `<ellipse />` element to draw a circle. For VML we just have `<v:oval />`.

### Circle size
SVG has special attributes for setting the size but in VML we set the `height` and `width` in `style`.

SVG `<circle />` just sets one value `r="90"` and `<ellipse />` has 2 `rx="90" ry="110.5"`

These values all set the size of the radius (measured from the centre point to the edge).
For VML we set the full height and width. So we need to multiple it by 2.

`rx="90"` ×2 = `width="180"`
`ry="110.5"` ×2 = `height="221"`


### Circle position
SVG has special attributes for setting the position but in VML we set the `top` and `left` in `style`, we also need to add `position: absolute;` here.

SVG sets the position using `cx="251" cy="167.5"`

SVG does positioning from the centre point of the circle, so again we need to do some conversion.  Subtract the width from the position and you'll get the VML position value.

`cx="251"` - `rx="90"` = `left:161`
`cy="167.5"` - `ry="110.5"` = `top:57`



## Custom shape
**SVG**
{% highlight html %}
<path d="M48 421.77 C48 250.077 453 250.076 453 421.77 V500 H48 V421.77Z" fill="#a8b3dc"/>
{% endhighlight %}

**VML**
{% highlight html %}
<v:shape path="M48 422 C48 250 453 250 453 422 L453 500 48 500 48 422 xe" fillcolor="#a8b3dc" stroked="f"/>
{% endhighlight %}

### Custom shape element
SVG uses a `path` element with the coordinates defined in a `d` attribute, and VML uses a `v:shape` element with with the coordinates defined in a `path` attribute.

### Custom shape path
The path is defined with a combination of letters and numbers.  The numbers are in pairs and give coordinates `x y` and the letters give meaning to those.

* `M` Move to. This sets the starting point. If you leave it off it will start at `0 0`.
* `L` Line to.
* `H` Horazontal line. This is a short cut that keeps the `y` coordinate. ######################################################################################################
* `V` Vertical line.
* `C` Curve. There are 6 values, think of them as 3 pairs of `x y`. The first pair control the start of the curve, the second pair control the end of the curve and the third pair set the end point.
* `Z` `XE`



## Colour
For all the above shapes we can add a fill colour. SVG uses `fill=""` VML uses `fillcolor=""` so it's pretty simple to convert. VML only supports setting colour as, 3 digit hex, 6 digit hex, colour names and rgb. So if the SVG is set any other way you will need to convert that.

If you need to set a transparent background with VML, you can use `fillcolor="none"`.

## Stroke
VML will always add a stroke by default.  SVG does not.  In the above examples I've added `stroked="f"` to remove the stroke however if you want to use it.  Then you can either leave that off or set it to `stroked="true"` then set the colour with `strokecolor="red"` and the thickness with `strokeweight="10"`.




## Accessibility
From what I've seen VML isn't very accessible.  I believe Outlook will actually renders the VML as an image and displays it in an `<img>` element. So you can see it but you can't interact with it.

Any links inside the VML aren't clickable for any users. But you can add an `href` to the outer element to make the whole object a link.

There is some attempt to create alt text based on any text inside but it is far from reliable, bits are missed.  However you can add an `alt` attribute to the outer element to pass alt text.



## Resources
https://yqnn.github.io/svg-path-editor/ Can help with rounding numbers, and adjusting for viewbox with 4 values.
