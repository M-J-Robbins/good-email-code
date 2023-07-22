# MSO Outlook background images
MSO versions of Outlook don't support `background-image`.  This is a real pain from a design point of view.  For a while now there has been a hack to get around this using VML, the good folks over at Campaign Monitor have even built a great tool to help generate the code [backgrounds.cm](https://backgrounds.cm/).

However there are a couple of issue with that work around.  You can't nest VML in this way, so if you were to try and place a background in a background, or use a VML button then it won't work.  But the bigger issue is accessibility.  Content inside VML can't be focused on with a keyboard input or a screen reader, meaning some users won't be able to access the content or click the links inside that section.

But there is another option...


## The Code
{% highlight html %}
<v:image src="https://placekitten.com/600/300" style="width:600px;height:300px;position:absolute;z-index:-1;mso-element-left:center;"/>
<h1>Email content</h1>
{% endhighlight %}

This is still a VML based solution, however instead of putting the content inside the VML, we are placing the VML behind the content.

### v:image
This is a VML property, you can read more about is in the [v:image VML docs](https://docs.microsoft.com/en-us/windows/win32/vml/msdn-online-vml-image-element).  Being VML this will only render in MSO versions of Outlook.  You can combine this with `background-image` to get support elsewhere.

### `position:absolute; z-index:-1;mso-element-left:center;`
Using `position:absolute` takes the image out of the flow of the template so the content below can sit directly in front of it.  Then we use `z-index:-1` to move the image behind the content.  This is similar to what we use for [faux absolute position](../email-enhancements/faux-absolute-position).

Then we centre the image using `mso-element-left:center;`, this is an MSO specific style for aligning block elements.

### Retina images
? compare to backgrounds.cm

## Gradient background
This can also be used to create gradient backgrounds.

{% highlight html %}
<v:rect fillcolor="blue" stroked="0"	style="width:600px;height:300px;position:absolute;z-index:-1;mso-element-left:center;">
  <v:fill type="gradient" color="blue" color2="red" angle="45"/>
</v:rect>
<h1>Email content</h1>
{% endhighlight %}

The concept is the same here except we're using a `v:rect` predefined shape, rather than a `v:image` but the styles remain the same.

### Gradient
The gradient

### Adding rounded corners
Rounded corners can be added by changing `v:rect` to `v:roundrect` and adding `arcsize`

{% highlight html %}
<v:roundrect arcsize="10%" fillcolor="blue" stroked="0"	style="width:600px;height:300px;position:absolute;z-index:-1;mso-element-left:center;">
  <v:fill type="gradient" color="blue" color2="red" angle="45"/>
</v:roundrect>
<h1>Email content</h1>
{% endhighlight %}

## Limitations
The biggest limitation here is that the image is a fixed size and doesn't scale with the content.  When used for a one off campaign then it's easy to make adjustments but it could be complicated for anything auto generated.



Is there a way to use v:background and make it fit to a container?
<v:background xmlns:v="urn:schemas-microsoft-com:vml" fill="t">
	<v:fill type="tile" src="https://i.imgur.com/YJOX1PC.png" color="#7bceeb"/>
</v:background>
