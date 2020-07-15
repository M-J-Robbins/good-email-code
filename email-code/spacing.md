# Spacing
Spacing seems like a very simple task but to do it accurately in email can get a little tricky at times.

Your first options should always be using `margin` or `padding`, [support for margin](https://www.caniemail.com/features/css-margin/) and [support for padding](https://www.caniemail.com/features/css-padding) is pretty good across emails clients with a few small issues in Outlook.

If you are still having issue then you can try these methods.

## Horizontal Spacer

### The Code
{% highlight html %}
<i style="letter-spacing:30px;mso-font-width:-100%;font-size:1px">&#8202;</i>
{% endhighlight %}

To get it working in MSO Outlooks we are using `letter-spacing` to create the size of this spacer. And for `letter-spacing` to work we need a letter for it to work off.  In this case we are using a _"Hair Space"_ `&#8202;`.  This is the thinest character I found so it only adds a very tiny amount of space onto the 30px specified in the `letter-spacing`.

In a lot of cases this extra space is probably acceptable, however if you want to remove it and get a more exact space you can add `mso-font-width:-100%;` to remove the space in MSO Outlooks, and `font-size:1px` to reduce the space in HTML email clients.  If you need it to be 100% exact then use `display:inline-block;width:30px`.

*em* values can be used here too, however you'll need to move the `font-size:1%` onto another element wrapping the `&#8202;` inside the spacer.

*Outlook 2013* seems to have some issues depending on the elements that are being spaced. If you have this issue, try changing `<i>` to `<span>`.

*IBM Notes 9* requires 2 characters to apply the spacing but then other clients apply it at twice the width.  If you need to support that, I'd recommend setting margin or padding on the items you want to space then apply the spacer for MSO outlooks only.
{% highlight html %}
<i style="display:none;mso-hide:none;letter-spacing:50px;mso-font-width:-100%;">&#8202;</i>
{% endhighlight %}



## Vertical Spacer

### The Code
{% highlight html %}
<div style="line-height:50px;">&#8202;</div>
{% endhighlight %}

Again we need to insert a character, this time to have something for the `line-height` to respond to and stop the `<div>` from collapsing.
