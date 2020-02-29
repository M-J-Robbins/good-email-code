# Preheader

This is a text snippet that appears under the subject line in the inbox but is hidden from the from the email when it's opened.

## The code
{% highlight html %}
<div style="display:none">
Preheader text here
</div>
{% endhighlight %}
Yup it's that simple.

Ok well there are a few other things worth mentioning.

##  Mail.ru
The mail.ru email client won't show text in the preheader if it's set to `display:none`, `visibility: hidden`, or has a `hidden` attribute.

So if you want to make it work in mail.ru we can use this code

{% highlight html %}
<div style="max-height:0;overflow:hidden;mso-hide:all;" aria-hidden="true">
  Preheader text here
</div>
{% endhighlight %}

For this we set the div to not take up any height space, and to hide the content that would overflow `max-height:0;overflow:hidden;`.  Then for MSO Outlook we can use the specific mso code `mso-hide:all;`. And finally as we want this code to be hidden in the email we also want it hidden for screen readers so we add `aria-hidden="true"`.

## Preheader spacing hack
If you want to use a short preheader then the rest of the space of the preheader will pull in content from the rest of your email.  To stop this happening we can fill the remaining space with... spaces.  For this just add a number of spaces with `&#847;` between them, like this `&#847; &#847; &#847; &#847; &#847; &#847; &#847; &#847;`.  Just add as many as you need to fill up the space.  You could also try using `&zwnj;` or `&#8204;` but from my tests those don't add any space on mail.ru

I've also heard reports of the code sometimes showing in the preheader, I've not been able to reproduce this but from what I've heard that might only happen when using `&zwnj;`.

## GMX apps
The GMX app pulls in preheader content from the plain text version of the email, if this version is generated with `&zwnj;` `&#847;` or `&#8204;` rather than the characters they represent then they will show in the preheader.  You may need to copy and paste the character into your plain text version, you can copy the [Combining Grapheme Joiner on unicode-table](https://unicode-table.com/en/034F/), remember to put a space between each time you paste it.
