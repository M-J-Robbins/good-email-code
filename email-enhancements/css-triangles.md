# CSS triangles
I originally wrote about this back in 2014 on my old site. So reposting with some small updates.

Essentially this is exactly as it sounds, a triangle shape made from CSS.
## The code
{% highlight html %}
<div style="border:2em solid transparent;border-top-color:red;border-bottom:none;display:inline-block"></div>
<!--[if mso]>
  <v:shape path="m,l1000,0 500,1000xe" style="width:60px;height:30px;mso-position-horizontal:center;" fillcolor="red" stroked="f"><o:lock selection="t"/></v:shape>
<![endif]-->
{% endhighlight %}

This code produces a small red triangle like this.
<div style="border:2em solid transparent;border-top-color:red;border-bottom:none;display:inline-block"></div>

We can make this point left, right, up or down and in in diagonal directions top left, top right, bottom right, bottom left.


### The CSS part
{% highlight html %}
<div style="border:2em solid transparent;border-top-color:red;border-bottom:none;display:inline-block"></div>
{% endhighlight %}

##  # The VML part 
{% highlight html %}
<!--[if mso]>
  <v:shape path="m,l1000,0 500,1000xe" style="width:60px;height:30px;mso-position-horizontal:center;" fillcolor="red" stroked="f"><o:lock selection="t"/></v:shape>
<![endif]-->
{% endhighlight %}
