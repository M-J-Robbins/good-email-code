# Faux Absolute Position
I originally wrote about this back in 2016 on the old Rebel site. More recently it has come up in a few conversations on (email geek slack)[https://email.geeks.chat/]. Shortly after I started work on this article I realised 2 other email geeks, Rémi Parmentier, Steven Sayo were writing their own too, so we decided to team up and cross reference each other.

You can read their articles here:
* *Rémi Parmentier ()[]*
* *Steven Sayo [Email Absolute Positioning](https://medium.com/@sayo1337/efd2f2f09ed4)*


## The code
With the code we are applying absolute positioning to some text so that it sits over an image.  You can adapt this to position anything you like over anything else in your email but be careful when moving or covering anything you want to be clickable.

{% highlight css %}
.faux-absolute{
  max-height:0;
  position:relative;
  opacity:0.999;
}
.faux-position{
  margin-top:5em;
  margin-left:1em;
  display:inline-block;
}
body[data-outlook-cycle] .image{
  width:300px;
}
{% endhighlight %}

{% highlight html %}
<div class="faux-absolute">
	<!--[if mso]>
	<v:rect xmlns:v="urn:schemas-microsoft-com:vml" stroked="false" filled="false" style="mso-width-percent: 1000; position:absolute; top:80px; left:16px;">
	<v:textbox inset="0,0,0,0">
	<![endif]-->
	<div class="faux-position">
		Faux Absolute Position content
	</div>
	<!--[if mso]>
	</v:textbox>
	</v:rect>
	<![endif]-->
</div>
<img src="https://placekitten.com/600/400" alt="" class="image" style="width:100%;max-width:37.5em">
{% endhighlight %}

The code above is broken up into CSS in the top snippet and HTML in the bottom. This gives us the most basic form of targeting for progressive enhancement.  

By default this will show the text positioned above the image, if an email client supports embedded styles then we should see the text positioned overlaid on top of the image.  I've done it this way partly to account for Gmail IMAP accounts (also referred to as GANGA) that don't support this method.  Also Mail.ru doesn't support opacity when set inline, but does accept it in the embedded styles.  

### faux-absolute
{% highlight css %}
.faux-absolute{
  max-height:0;
  position:relative;
  opacity:0.999;
}
{% endhighlight %}
{% highlight html %}
<div class="faux-absolute">
{% endhighlight %}

In the HTML, you'll see a div with a class of faux-absolute and the corresponding CSS above.  Here I've applied `max-height:0;`, this means that this element, along with any content, will take up no vertical space in the email.  This is really where the magic lies in this trick, the content is taking up no vertical space so the content below will sit directly on top of it (feel free to add `max-width:0;` too if you need to remove horizontal space).

However this content is now sitting behind the following content.  In our case the text is behind the image. So now we need to increase the `z-index` so it sits on top.  We don't actually need to set a value on the z-index (support isn't great here) we just need to enable it, for this we use `position:relative;`.  

Unfortunately a lot of email clients don't support that, so we can also enable z-index with opacity so we set `opacity:0.999;`. This does mean the content will be slightly transparent but it's unlikely to be visible to human eyes.  Also don't be tempted to try and up that to `0.9999` or higher as mail.ru will round this up to `opacity:1` so we have to keep it limited to 3 decimal places.

### faux-position
{% highlight css %}
.faux-position{
  margin-top:5em;
  margin-left:1em;
  display:inline-block;
}
{% endhighlight %}
{% highlight html %}
<div class="faux-position">
{% endhighlight %}
This is where we apply the code to move our content to a more exact position.  We apply `margin-top` to set the position from the top and `margin-left` to set the position from the left.

If you want to position from the right instead of the left firstly add `float:right` then set the position with `margin-right`..

It's also important to set `display:inline-block` so these margins are placed against the parent `faux-absolute` div rather than combining with it.

### The Outlook bit
{% highlight html %}
<!--[if mso]>
	<v:rect xmlns:v="urn:schemas-microsoft-com:vml" stroked="false" filled="false" style="mso-width-percent: 1000; position:absolute; top:80px; left:16px;">
	<v:textbox inset="0,0,0,0">
<![endif]-->
	Faux Absolute Position content
<!--[if mso]>
	</v:textbox>
	</v:rect>
<![endif]-->
{% endhighlight %}

For Outlook we can actually use regular CSS absolute positioning, which may surprise you to have this more advanced CSS support in Outlook.  However there is a catch.  Outlook does support absolute positioning but only when done inside VML.

So here inside conditional comments `<!--[if mso]><![endif]-->` we've set a very basic VML shape `<v:rect>` initially I used `<v:shape>` but that didn't work on Windows 10 Mail.  This shape is set to `stroked="false" filled="false"` so it has no outline or background, and set to `mso-width-percent: 1000;` which rather confusingly means 100% not 1000%.  No height is needed here.

I then set `position:absolute; top:80px; left:16px;` just as if we were building a web page.  However I should point out that `em` units don't work inside VML so I've switched to `px`.

*NB* VML has some accessibility issue.  [Links are not keyboard accessible when inside VML](https://github.com/hteumeuleu/email-bugs/issues/77) so be carful about the content you use inside this.  If you leave the VML off then the text will sit on top of the image.

### The image
{% highlight css %}
body[data-outlook-cycle] .image{
  width:300px;
}
{% endhighlight %}
{% highlight html %}
<img src="https://placekitten.com/600/400" alt="" class="image" style="width:100%;max-width:37.5em">
{% endhighlight %}
I've included an image in this code partly to have something for our absolute positioned text to appear over, but also to demonstrate a potential issue.

In Outlook mobile apps, if an image width is set to be wider than the viewport, Outlook will apply a `transform: scale()` to make it fit.  Even if you have `max-width:100%` to make it responsive. By applying this it can affect the z-index and place the image over the text.  So to fix the issue we need to apply a fixed width to the image. I've done this using `body[data-outlook-cycle] .image` so that it will only apply to Outlook mobile apps.



## Related content
I hope that was helpful now go and check out
* Rémi Parmentier...
* Steven Sayo [Email Absolute Positioning](https://medium.com/@sayo1337/efd2f2f09ed4)
