# Spacing
Spacing seems like a very simple task but to do it accurately in email can get a little tricky at times.

Your first options should always be using `margin` or `padding`, [support for margin](https://www.caniemail.com/features/css-margin/) and [support for padding](https://www.caniemail.com/features/css-padding) is pretty good across emails clients with a few small issues in Outlook.

If you are still having issue then you can try these methods.

## Horizontal Spacer

### The Code
{% highlight html %}
<i style="letter-spacing:30px;mso-font-width:-100%;display:inline-block;width:30px">&#8202;</i>
{% endhighlight %}

To get it working in MSO Outlooks we are using `letter-spacing` to create the size of this spacer. And for `letter-spacing` to work we need a letter for it to work off.  In this case we are using a _"Hair Space"_ `&#8202;`.  This is the thinest character I found so it only adds a very tiny amount of space onto the 30px specified in the `letter-spacing`.  To remove that spacing from MSO Outlooks we can use `mso-font-width:-100%;`

For HTML email clients we can add `display:inline-block;width:30px`.


## Vertical Spacer

### The Code
{% highlight html %}
<div style="line-height:50px;">&#8202;</div>
{% endhighlight %}

Again we need to insert a character, this time to have something for the `line-height` to respond to and stop the `<div>` from collapsing.
