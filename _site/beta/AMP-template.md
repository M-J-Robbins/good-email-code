# Email Template

This is a simple stripped back basic AMP for email template that I'd use for every AMP email I send.

## The code
{% highlight html %}
<!DOCTYPE html>
<html ⚡4email data-css-strict lang="en">
<head>
<meta charset="utf-8">
<script async src="https://cdn.ampproject.org/v0.js"></script>
<style amp4email-boilerplate>body{visibility:hidden}</style>
<style amp-custom>

</style>
</head>
<body>
  <article aria-roledescription="email" aria-label="email name" style="font-size:1rem">
    <!-- email content in here -->
  </article>
</body>
</html>
{% endhighlight %}
If you want to just copy and paste that code you are welcome to, just be sure to edit the content in the `lang` attributes, `charset`, `aria-label`.

If you are interested in the reasons behind why each part of the code is there, read on and I'll break it down in more detail.

## Doctype
{% highlight html %}
<!DOCTYPE html>
{% endhighlight %}
Here we're using an HTML5 Doctype, this is the only one supported in AMP for email.


## HTML element
{% highlight html %}
<html ⚡4email data-css-strict lang="en">
{% endhighlight %}
The `<html>` tag defines the document as HTML format.

### ⚡4email
This attribute defines this is the AMP for email format. We can also use `Amp4email` rather than `⚡4email`.  

I prefer `⚡4email` as it strands out more, but using the text version `Amp4email` may help if the `⚡` symbol causes issues with your ESP.

<!-- ### data-css-strict
(tbc) -->

### Lang
This sets the language of the email, it's important to set as this can affect the way email clients, browsers, screen readers and other assistive technology interpret your content. You can use multiple languages in the same email but it's important to only set one as the default.  After that you can place a lang attribute on any element where the language changes from the default.

Here I've set `lang="en"` to set the content in English, however you can get more granular if you like and set `en-GB` for British English or `en-US` for American English.

Read more on the [w3school lang attribute page](https://www.w3schools.com/tags/att_global_lang.asp), they also have a useful [list of language codes](https://www.w3schools.com/tags/ref_language_codes.asp).

## Meta
There are a lot of restrictions on allowed `<meta>` in AMP for email but it's also worth noting most of these wouldn't do anything even if they were supported as the email will only ever live in the inbox and not online.

### charset
{% highlight html %}
<meta charset="utf-8">
{% endhighlight %}
This sets the character encoding standard which can limit the character that are used.  Unlike the lang attribute we can only set one charset for the file.

### author
{% highlight html %}
<meta name="author" content="Mark Robbins">
{% endhighlight %}
One `<meta>` that is allowed is author, although in email the sender address tends to inform the user who created the email.  It could be used internally so other editors know who authored the fist version.

<!-- ### color-scheme
Are supported but too early to tell if they will be needed. -->

## Title
Amp emails do not have a `<title>` element as they are not meant to be seen outside of the inbox.  So this title will never be seen.


## Script
{% highlight html %}
<script async src="https://cdn.ampproject.org/v0.js"></script>
{% endhighlight %}
AMP for email work off JavaScript.


## Style
{% highlight html %}
<style amp4email-boilerplate>body{visibility:hidden}</style>
<style amp-custom>

</style>
{% endhighlight %}



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
