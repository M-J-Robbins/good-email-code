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


### The CSS part
{% highlight html %}
<div style="border:2em solid transparent;border-top-color:red;border-bottom:none;display:inline-block"></div>
{% endhighlight %}

The concept here is, if we set borders on an element that has no height or width, then the 4 sides of the border will take the shape of 4 triangles.  We can see this if we set a different colour on each side.
<div style="border:2em solid transparent;border-top-color:red;border-right-color:green;border-bottom-color:blue;border-left-color:yellow;display:inline-block"></div>

So there are a number of ways to write the code but this is the simplest I've found.  Start by setting a transparent boarder `border:2em solid transparent` then colour one side `border-top-color:red;` and remove the space from the opposite side `border-bottom:none;` and set the element to `display:inline-block`.

To get a diagonal arrow, simple put 2 sides together, here I am using top and left
{% highlight html %}
<div style="border:2em solid transparent;border-top-color:red;border-left-color:red;display:inline-block"></div>
{% endhighlight %}
<div style="border:2em solid transparent;border-top-color:red;border-left-color:red;display:inline-block"></div>


##  # The VML part
{% highlight html %}
<!--[if mso]>
  <v:shape path="m,l1000,0 500,1000xe" style="width:64px;height:32px;mso-position-horizontal:center;" fillcolor="red" stroked="f"><o:lock selection="t"/></v:shape>
<![endif]-->
{% endhighlight %}
