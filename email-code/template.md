# Email Template

This is a simple stripped back basic template that I'd use for every email I send.

## The code
{% highlight html %}
<!DOCTYPE html>
<html lang="en" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="format-detection" content="telephone=no">
<meta name="format-detection" content="date=no">
<meta name="format-detection" content="address=no">
<meta name="format-detection" content="email=no">
<meta name="x-apple-disable-message-reformatting">
<meta name="color-scheme" content="light only">
<meta name="supported-color-schemes" content="light only">
<title>Email title</title>
<!--[if mso]>
<xml>
<o:OfficeDocumentSettings>
  <o:AllowPNG/>
  <o:PixelsPerInch>96</o:PixelsPerInch>
</o:OfficeDocumentSettings>
</xml>
<![endif]-->
<style>
:root {
  color-scheme: light only;
  supported-color-schemes: light only;
}
</style>
</head>
<body class="body">
<div role="article" aria-roledescription="email" aria-label="email name" lang="en">
<!-- email content in here -->
</div>
</body>
</html>
{% endhighlight %}
If you want to just copy and paste that code you are welcome to, just be sure to edit the content in the lang attributes, charset, title, aria-label.  

If you are interested in the reasons behind why each part of the code is there, read on and I'll break it down in more detail.

## Doctype
{% highlight html %}
<!DOCTYPE html>
{% endhighlight %}
Here we're using an HTML5 Doctype.  I still see a lot of people using HTML4 but I'd always recommend HTML5.  Not every email client will respect the doctype you set, some will remove it and use their own, but that is mostly HTML5, so if we set HTML5 for the few that doo look for it we get more consistent rendering.  

Rémi Parmentier has written a really great article about [Which doctype should you use in HTML emails](https://emails.hteumeuleu.com/which-doctype-should-you-use-in-html-emails-cd323fdb793c).  If you want to know more I'd strongly recommend reading that.

## HTML element
{% highlight html %}
<html lang="en" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
{% endhighlight %}
The `<html>` tag defines the document as HTML format, however if the files is saves as `.html` then this is assumed anyway so it's not really needed.  However what is needed are the attributes set on in.

### Lang
This sets the language of the email, it's important to set as this can affect the way email clients, browsers and screen readers and other assitive technology interpret your content. You can use multiple languages in the same email but it's important to only set one as the default.  After that you can place a lang attribute on any element where the language changes from the default.

As email clients often strip the `<html>` element it's also important to set a lang on the [Wrapping element](#wrapping-element).

Read more on the [w3school lang attribute page](https://www.w3schools.com/tags/att_global_lang.asp).

## Meta
There are a number of meta elements that we set here so lets look at them individually.

### charset
{% highlight html %}
<meta charset="utf-8">
{% endhighlight %}
This sets the character encoding standard which can limit the character that are used.  Unlike the lang attribute we can only set one charset for the file.

I need to set some time to look into this more but generally i believe utf-8 should cover most cases.

Be aware that the email headers may override what is set in the meta.

### http-equiv
{% highlight html %}
<meta http-equiv="X-UA-Compatible" content="IE=edge">
{% endhighlight %}
This tells the browser which version of IE to render with.  In theory this would only apply to webmail clients opening in IE 9 or below (although meta tags are likely to be stripped from webmail), emails viewed in browser in IE 9 or below and Outlook 2000-2003 for windows.  

It also enables media queries to work on some versions of windows phone.

As the years go on I think it's getting safer and safer to remove this meta tag.

### Viewport
{% highlight html %}
<meta name="viewport" content="width=device-width,initial-scale=1">
{% endhighlight %}
The viewport element gives the browser and email client instructions on how to control the page's dimensions and scaling.  `width=device-width` sets the width of the page to follow the screen-width of the device.  `initial-scale=1.0` sets the initial zoom level when the page is first loaded by the browser.

### Format detection
{% highlight html %}
<meta name="format-detection" content="telephone=no">
<meta name="format-detection" content="date=no">
<meta name="format-detection" content="address=no">
<meta name="format-detection" content="email=no">
{% endhighlight %}
In theory these prevent email clients automatically detecting and generating links out of phone numbers, dates, addresses and email addresses.
However support is low, I've only ever seen it work for phone numbers on the Outlook iOS app.  I'd recommend including these anyway as it's a hint to the email clients that this is something we want.

There is also a debate about weather this is a user experience enhancement that users want and that it shouldn't be blocked.  But I think there are too many issues with the auto detection to reply on it so I feel like it should be blocked.


### x-apple-disable-message-reformatting
{% highlight html %}
<meta name="x-apple-disable-message-reformatting">
{% endhighlight %}
As the name suggests this is specific to Apple.  It appears Apple were trying to fix the display of non-responsive email in their iOS email client, however when encountering a responsive email they would display at half the width of the screen and zoomed out.  This meta tag prevents the Apple fix and relies on the developer to make the email responsive.

There are more details on [Apple auto-scaling emails bug](https://github.com/hteumeuleu/email-bugs/issues/18) on the email bugs repo.


### color-scheme
{% highlight html %}
<meta name="color-scheme" content="light only">
<meta name="supported-color-schemes" content="light only">
{% endhighlight %}
These are used to control dark mode preferences. They both do the same thing but `supported-color-schemes` was renames to `color-scheme` so for now we include both to get more as the old name is supported by WebKit, Safari, and Mail in macOS 10.14.4.

The `content` values are
* light dark — tells the email clients that both light and dark mode are coded and ready to use.
* only - tells the email clients that only light mode is ready to use and not to try and transform light styles.
* light dark only — The UA will choose the first of the listed schemes that it supports taking user preference into account, and never apply transformations.

I tend to default to `light only` then control dark styles with a `prefers-color-scheme` media query.


## Title
{% highlight html %}
<title>Email title</title>
{% endhighlight %}
The title element give a title to your document, this will be seen in the browser tab, if a user selects to view the email in a browser.  I have previously seen the title show in a preview for the old default Android client, it's possible that something like that may happen again.

## XML
{% highlight html %}
<!--[if mso]>
<xml>
  <o:OfficeDocumentSettings>
    <o:AllowPNG/>
    <o:PixelsPerInch>96</o:PixelsPerInch>
  </o:OfficeDocumentSettings>
</xml>
<![endif]-->
{% endhighlight %}
This code helps rendering on Windows versions of Outlook desktop.
`<!--[if mso]> <![endif]-->` This if statement means this code is only visible to Windows versions of Outlook desktop.
`<o:AllowPNG/>` This improves support for PNG images.
`<o:PixelsPerInch>96</o:PixelsPerInch>` This will improve rendering on machines that have a higher DPI set, this is often the case for Windows machines that have higher than standard resolution  monitors.

## Style
{% highlight html %}
<style>
  :root {
    color-scheme: light only;
    supported-color-schemes: light only;
  }
</style>
{% endhighlight %}
This is essentially a duplicate of the [meta color-scheme](#color-scheme). At time of writing this only really works in Apple Mail which supports both methods but in the interest of future proofing I'm including both.  There is also a potential argument to apply this to the wrapping element too.

## Body
{% highlight html %}
<body class="body">
{% endhighlight %}
I always like to define a body class on the body element, this is because sometimes when an email renders the `<body>` element is converted to a `<div>`.  It is also useful for targeting certain email clients.

## Wrapping element
{% highlight html %}
<div role="article" aria-roledescription="email" aria-label="email name" lang="en">
{% endhighlight %}
Inside the email body we wrap the whole content of the email in this `<div>`, I've also seen some people appoly these attributes to a wrapping `<table>` personally I try and avoid tables as much as possible, but if that's your set up then you can use a `<table>`.

So taking a closer look at the attributes;
### role="article"
This is an accessibility enhancement, when navigating with a screen reader this will define the content as an article which the user will understand as something that can stand alone outside the context of the rest of the page.

### aria-roledescription="email"
We define this as stand alone content but it will be described as a article which may not be the best name for what the content is, so here we change that to say this is an email.

### aria-label="email name"
So we've said this is stand along content, we've said the content type is email now we give that a title.  I'd recommend using something like the subject line, or perhaps say who the email is from.

### lang="en"
This is a duplication of the [lang](#lang) set on the HTML element.  Email clients will often remove the `<html>` element so it's best to duplicateit here also.
