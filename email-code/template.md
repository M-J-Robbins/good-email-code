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
  <meta name="format-detection" content="telephone=no, date=no, address=no, email=no, url=no">
  <meta name="x-apple-disable-message-reformatting">
  <meta name="color-scheme" content="light dark">
  <meta name="supported-color-schemes" content="light dark">
  <title>Email title</title>
  <!--[if mso]>
  <noscript>
    <xml>
      <o:OfficeDocumentSettings>
        <o:PixelsPerInch>96</o:PixelsPerInch>
      </o:OfficeDocumentSettings>
    </xml>
  </noscript>
  <![endif]-->
  <style>
    :root {
      color-scheme: light dark;
      supported-color-schemes: light dark;
    }
  </style>
</head>
<body class="body">
  <div role="article" aria-roledescription="email" aria-label="email name" lang="en" style="font-size:1rem">
    <!-- email content in here -->
  </div>
</body>
</html>
{% endhighlight %}
If you want to just copy and paste that code you are welcome to, just be sure to edit the content in the `lang` attributes, `charset`, `title`, `aria-label`.

If you are interested in the reasons behind why each part of the code is there, read on and I'll break it down in more detail.

## Doctype
{% highlight html %}
<!DOCTYPE html>
{% endhighlight %}
Here we're using an HTML5 Doctype.  Not every email client will respect the doctype you set, some will remove it and use their own, but that is mostly HTML5 anyway. There are small rendering differences between HTML4 and HTML5, the most common one email devs notice is, you can't set a `<td>` to `display:block` in HTML4.

Rémi Parmentier has written a really great article about [which doctype should you use in HTML emails](https://emails.hteumeuleu.com/which-doctype-should-you-use-in-html-emails-cd323fdb793c).  If you want to know more I'd strongly recommend reading that.

## HTML element
{% highlight html %}
<html lang="en" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office">
{% endhighlight %}
The `<html>` tag defines the document as HTML format, however if the file is saved as `.html` then this is assumed anyway so it's not really needed.  However what is needed are the attributes set on in.

### Lang
This sets the language of the email, it's important to set as this can affect the way email clients, browsers, screen readers and other assistive technology interpret your content. You can use multiple languages in the same email but it's important to only set one as the default.  After that you can place a lang attribute on any element where the language changes from the default.

Here I've set `lang="en"` to set the content in English, however you can get more granular if you like and set `en-GB` for British English or `en-US` for American English.

As email clients often strip the `<html>` element it's also important to set a lang on the [Wrapping element](#wrapping-element).

Read more on the [w3school lang attribute page](https://www.w3schools.com/tags/att_global_lang.asp), they also have a useful [list of language codes](https://www.w3schools.com/tags/ref_language_codes.asp).

## Meta
There are a number of meta elements set here so lets look at them individually.

### charset
{% highlight html %}
<meta charset="utf-8">
{% endhighlight %}
This sets the character encoding standard which can limit the character that are used.  Unlike the lang attribute we can only set one charset for the file.

I need to set some time to look into this more but generally I believe utf-8 should cover most cases.

Be aware that the email headers may override what is set in the meta.

### http-equiv
{% highlight html %}
<meta http-equiv="X-UA-Compatible" content="IE=edge">
{% endhighlight %}
This tells the browser which version of IE to render with.  In theory this would only apply to webmail clients opening in IE 9 or below (although meta tags are likely to be stripped from webmail), emails viewed in browser in IE 9 or below and Outlook 2000-2003 for windows.  

It also enables media queries to work on some versions of windows phone.

As the years go on I think it's getting safer and safer to remove this meta tag.

### viewport
{% highlight html %}
<meta name="viewport" content="width=device-width,initial-scale=1">
{% endhighlight %}
The viewport element gives the browser and email client instructions on how to control the page's dimensions and scaling.  `width=device-width` sets the width of the page to follow the screen-width of the device.  `initial-scale=1.0` sets the initial zoom level when the email is first loaded.

### format-detection
{% highlight html %}
<meta name="format-detection" content="telephone=no, date=no, address=no, email=no, url=no">
{% endhighlight %}
In theory these prevent email clients automatically detecting and generating links out of phone numbers, dates, addresses, email addresses and url's.
However support is low, I've only ever seen it work for phone numbers on the Outlook iOS app.  I'd recommend including these anyway as it's a hint to the email clients that this is something we want.

There is an argument that we shouldn't use these as the auto linking helps users.  However I feel there are too many issues with the auto detection to reply on it, if I add a phone number I will add a link myself. If I include numbers for another reason (order number etc.) I don't want them linking to a phone number.

### x-apple-disable-message-reformatting
{% highlight html %}
<meta name="x-apple-disable-message-reformatting">
{% endhighlight %}
As the name suggests this is specific to Apple.  It appears Apple were trying to fix the display of non-responsive email in their iOS email client, however when encountering a responsive email they would display at half the width of the screen and zoomed out.  This meta tag prevents the Apple fix and relies on the developer to make the email responsive.

There are more details on [Apple auto-scaling emails bug](https://github.com/hteumeuleu/email-bugs/issues/18) on the email bugs repo.


### color-scheme
{% highlight html %}
<meta name="color-scheme" content="light dark">
<meta name="supported-color-schemes" content="light dark">
{% endhighlight %}
These are used to control dark mode preferences. They both do the same thing but `supported-color-schemes` was renamed to `color-scheme` so for now we include both to get more as the old name is supported by Safari, and Mail in macOS 10.14.4.

The `content` values are
* light - tells the email client that only light styles are provided
* light only - tells the email clients that only light mode styles are ready to use and not to try and transform them to dark.
* light dark — tells the email clients that both light and dark styles are coded and ready to use.
* light dark only — tells the email clients that light and dark styles are ready to use and not to try and transform light styles.

It's best to set this with logic depending on if dark styles are included in the code. But if you can't place that logic I'd opt for `light dark`.


## Title
{% highlight html %}
<title>Email title</title>
{% endhighlight %}
The title element give a title to your document, this will be seen in the browser tab if a user selects to view the email in a browser.  I have previously seen the title show in a preview for the old default Android client, it's possible that something like that may happen again.

## XML
{% highlight html %}
<!--[if mso]>
<noscript>
  <xml>
    <o:OfficeDocumentSettings>
      <o:PixelsPerInch>96</o:PixelsPerInch>
    </o:OfficeDocumentSettings>
  </xml>
</noscript>
<![endif]-->
{% endhighlight %}
This code helps rendering on Windows versions of Outlook desktop.
* `<!--[if mso]> <![endif]-->` This if statement means this code is only visible to Windows versions of Outlook desktop. Although T-online also renders the code.
* `<noscript>` Stops the text `96` showing in T-Online.
* `<o:PixelsPerInch>96</o:PixelsPerInch>` This will improve rendering on machines that have a higher DPI set, this is often the case for Windows laptops that have higher than standard resolution monitors, or users who have manually chosen to increase the DPI.

## Style
{% highlight html %}
<style>
  :root {
    color-scheme: light dark;
    supported-color-schemes: light dark;
  }
</style>
{% endhighlight %}
This is essentially a duplicate of the [meta color-scheme](#color-scheme). At time of writing this only really works in Apple Mail which supports both methods but in the interest of future proofing I'm including both.  

## Body
{% highlight html %}
<body class="body">
{% endhighlight %}
I always like to define a body class on the body element, this is because sometimes when an email renders the `<body>` element is converted to a `<div>`.  It is also useful for targeting certain email clients.

## Wrapping element
{% highlight html %}
<div role="article" aria-roledescription="email" aria-label="email name" lang="en" style="font-size:1rem">
{% endhighlight %}
Inside the email body we wrap the whole content of the email in this `<div>`, I've also seen some people apply these attributes to a wrapping `<table>` personally I try and avoid tables as much as possible, but if that's your set up then you can use it on a `<table>`.

So taking a closer look at the attributes;
### `role="article"`
This is an accessibility enhancement, when navigating with a screen reader this will place the email into the landmarks menu and define the content as an article.  Although it may not be an article as such, the definition here is something that can stand alone outside the context of the rest of the page. And email fits that description.

### `aria-roledescription="email"`
As I mentioned previously, article may not be the best word to describe the content, so this will rename it to email.  This is a custom name so we can use anything here but I wouldn't advise using anything else apart from translating it to match the language of your content.  If you are unable to translate this to match your content I'd recommend leaving it off.

### `aria-label="email name"`
So we've said this is stand-alone content, we've said the content type is email now we give that a title.  To keep it simple I'd recommend using the subject line if you can dynamically insert that or perhaps say who the email is from.

### `lang="en"`
This is a duplication of the [lang](#lang) set on the HTML element.  Email clients will often remove the `<html>` element so it's best to duplicate it here also.

### `font-size: 1rem`
Some email clients may force a font-size on your email content. This resets it to be relative to the users settings so better for accessibility.  Ideally all other units in the email should be `em` so they are relative to this.

Most email clients and web browsers use a default font-size of 16px or larger but Apple mail uses a default of 12px. If you want to increase this default but still respect the the user settings then you can use `font-size:1rem; font-size:max(1rem, 16px)`.  If the user has a setting smaller than 16px then the font-size will be set to 16px, if it's larger then the rem value will be used.  If `max` isn't supported then it will fallback to the previous setting of `font-size:1rem;`.

Unfortunately rem units don't work everywhere if you want to find out more look at [email client support for rem units](https://www.caniemail.com/features/css-unit-rem/) and [browser support for rem units](https://caniuse.com/#feat=rem)
