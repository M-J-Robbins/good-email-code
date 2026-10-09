---
layout: default
title: Base Template
description: A base template to wrap all the email content in.
group: "code"
order: 1.1
--- 

<div class="updated">Last Updated: <time datetime="2026-10-09">09<sup>th</sup> October 2026</time></div>

# Base Template

This is a simple stripped back basic template that I'd use for every email I send.


## The code
```html
<!DOCTYPE html>
<html lang="en" dir="ltr" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:w="urn:schemas-microsoft-com:office:word">
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="format-detection" content="telephone=no, date=no, address=no, email=no, url=no">
  <meta name="x-apple-disable-message-reformatting" content="true">
  <meta name="color-scheme" content="light dark">
  <title>Email title</title>
  <!--[if mso]>
  <noscript>
    <xml>
      <o:OfficeDocumentSettings>
        <o:PixelsPerInch>96</o:PixelsPerInch>
      </o:OfficeDocumentSettings>
      <w:WordDocument>
        <w:DontUseAdvancedTypographyReadingMail/>
      </w:WordDocument>
    </xml>
  </noscript>
  <![endif]-->
  <style>
    :root {
      color-scheme: light dark;
    }
  </style>
</head>
<body class="body" xml:lang="en">
  <div role="article" aria-roledescription="email" aria-label="email subject line" lang="en" dir="ltr" style="font-size:medium; font-size:max(16px, 1rem)">
    <!-- email content in here -->
  </div>
</body>
</html>
```
If you want to just copy and paste that code you are welcome to, just be sure to edit the content in the `lang`, `dir` attributes, `charset`, `title`, `aria-label`.

If you are interested in the reasons behind why each part of the code is there, read on and I'll break it down in more detail.

## Doctype
```html
<!DOCTYPE html>
```
Here we're using an HTML5 Doctype.  Not every email client will respect the doctype you set, some will remove it and use their own, but that is mostly HTML5 anyway. There are small rendering differences between HTML4 and HTML5, the most common one email devs notice is, you can't set a `<td>` to `display:block` in HTML4.

Rémi Parmentier has written a really great article about [which doctype should you use in HTML emails](https://emails.hteumeuleu.com/which-doctype-should-you-use-in-html-emails-cd323fdb793c).  If you want to know more I'd strongly recommend reading that.

## HTML element
```html
<html lang="en" dir="ltr" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:w="urn:schemas-microsoft-com:office:word">
```
The `<html>` tag defines the document as HTML format, however if the file is saved as `.html` then this is assumed anyway so it's not really needed.  However what is needed are the attributes set on in.

### Lang
This sets the language of the email, it's important to set as this can affect the way email clients, browsers, screen readers and other assistive technology interpret your content. You can use multiple languages in the same email but it's important to only set one as the default.  After that you can place a lang attribute on any element where the language changes from the default.

Here I've set `lang="en"` to set the content in English, however you can get more granular if you like and set `en-GB` for British English or `en-US` for American English.

It's important to be accurate with your language settings, however if you are in the situation that you don't know what language will be used in your template you can use `lang="und"` which [defines the language as undetermined](https://iso639-3.sil.org/code/und). This can be used alongside `dir="auto"` to allow the direction to adapt to the language that is assumed.

In my testing I've found that using `lang="und" dir="auto"` did pick up the corrrect language and direction. However, this should only be used as a last resort, it’s nowhere near as good as setting these values explicitly, but it is better than not setting them at all.

As email clients often strip the `<html>` element it's also important to set a lang on the [Wrapping element](#wrapping-element). And for Windows Outlook we also need to set it on the [body](#body) as an `xml:lang`.

Read more on the [w3school lang attribute page](https://www.w3schools.com/tags/att_global_lang.asp), they also have a useful [list of language codes](https://www.w3schools.com/tags/ref_language_codes.asp).

### dir
This sets the language direction either as left to right (`ltr`) or right to left (`rtl`).

### xmlns 
These 3 settings are used to help Windows Outlook support. The `v`, `o` and `w` are used to prefix tags like `<v:rect>`, `<o:OfficeDocumentSettings>` and `<w:WordDocument>`. 
 * `xmlns:v="urn:schemas-microsoft-com:vml"` is needed if you want to use VML in your markup. I generally advice against using VML so I tend to exclude this one. Also if you prefer this can be placed [diretly on the VML](../email-enhancements/svg-to-vml#xmlns) shapes you use. 
 * `xmlns:o="urn:schemas-microsoft-com:office:office"` is used in the [XML](#xml) tags below that fix scaling issues.
 * `xmlns:w="urn:schemas-microsoft-com:office:word"` is used in the [XML](#xml) tags below that fix scaling text rendering issues.

## Meta
There are a number of meta elements set here so lets look at them individually.

### charset
 ```html
<meta charset="utf-8">
 ```
This sets the character encoding standard which can limit the character that are used.  Unlike the lang attribute we can only set one charset for the file.

Generally I would always use `utf-8` which covers almost all of the characters and symbols in the world.

Be aware that the email headers may override what is set in the meta.


### viewport
 ```html
<meta name="viewport" content="width=device-width, initial-scale=1">
 ```
The viewport element gives the browser and email client instructions on how to control the page's dimensions and scaling.  `width=device-width` sets the width of the page to follow the screen-width of the device.  `initial-scale=1.0` sets the initial zoom level when the email is first loaded.  

**Update:** Removed [user-scalable](#user-scalable)

### format-detection
 ```html
<meta name="format-detection" content="telephone=no, date=no, address=no, email=no, url=no">
 ```
In theory these prevent email clients automatically detecting and generating links out of phone numbers, dates, addresses, email addresses and url's.
However support is low, I've only ever seen it work for phone numbers on the Outlook iOS app.  I'd recommend including these anyway as it's a hint to the email clients that this is something we want.

There is an argument that we shouldn't use these as the auto linking helps users.  However I feel there are too many issues with the auto detection to rely on it, if I add a phone number I will add a link myself. If I include numbers for another reason (order number etc.) I don't want that linking to a phone number.

### x-apple-disable-message-reformatting
 ```html
<meta name="x-apple-disable-message-reformatting" content="true">
 ```
As the name suggests this is specific to Apple.  It appears Apple were trying to fix the display of non-responsive email in their iOS email client, however when encountering a responsive email they would display at half the width of the screen and zoomed out.  This meta tag prevents the Apple fix and relies on the developer to make the email responsive.

Including `content="true"` is required to make this valid HTML. I've seen this work without that addition, however including it reduces risk of it being stripped by an ESP or email client.

There are more details on [Apple auto-scaling emails bug](https://github.com/hteumeuleu/email-bugs/issues/18) on the email bugs repo.


### color-scheme
 ```html
<meta name="color-scheme" content="light dark">
 ```

These are used to control dark mode preferences. 

The `content` values include
* light - tells the email client that only light styles are provided
* dark - tells the email client that only dark styles are provided
* light only - tells the email clients that only light mode styles are ready to use and not to try and transform them to dark.
* dark only - tells the email clients that only dark mode styles are ready to use and not to try and transform them to dark.
* light dark — tells the email clients that both light and dark styles are coded and ready to use.
* light dark only — tells the email clients that light and dark styles are ready to use and not to try and transform any styles.

It's best to set this with logic depending on if dark styles are included in the code. But if you can't place that logic I'd opt for `light dark`.

#### Gmail color-scheme
  ```html
<meta name="color-scheme" content="light only">
 ```
Setting this will prevent Gmail from applying it's forced dark mode styles to the email. It's advised not to use this and instead work with the dark styles to respect the users preference. However sometimes the changes made by Gmail can create accessibility issues and this is a quick way to sort that.

Setting this also has a knock on effect and will prevent AppleMail showing dark styles you have provided. This Apple issue can be fixed by [setting the `color-scheme` in CSS](#style) to `light dark` as Gmail will ignore these styles.


## Title
 ```html
<title>Email title</title>
 ```
The title element give a title to your document, this will be seen in the browser tab if a user selects to view the email in a browser.  I have previously seen the title show in a preview for the old default Android client, it's possible that something like that may happen again.

## XML
 ```html
<!--[if mso]>
<noscript>
  <xml>
    <o:OfficeDocumentSettings>
      <o:PixelsPerInch>96</o:PixelsPerInch>
    </o:OfficeDocumentSettings>
    <w:WordDocument>
      <w:DontUseAdvancedTypographyReadingMail/>
    </w:WordDocument>
  </xml>
</noscript>
<![endif]-->
 ```
This code helps rendering on Windows versions of Outlook desktop.
* `<!--[if mso]> <![endif]-->` This if statement means this code is only visible to Windows versions of Outlook desktop. Although T-online also renders the code.
* `<noscript>` Stops the text `96` showing in T-Online.
* `<o:PixelsPerInch>96</o:PixelsPerInch>` This will improve rendering on machines that have a higher DPI set, this is often the case for Windows laptops that have higher than standard resolution monitors, or users who have manually chosen to increase the DPI.
* `<w:DontUseAdvancedTypographyReadingMail/>` This prevents text rendering inconsistencies with adaptive justification, kerning, ligatures and hyphenation in Outlook. 

## Style
 ```html
<style>
  :root {
    color-scheme: light dark;
  }
</style>
 ```
This is essentially a duplicate of the [meta color-scheme](#color-scheme). If you are setting the `light only` value for the meta tag to prevent Gmail forced dark mode. Then you can set a different value here in CSS there will override the meta value in clients like AppleMail. 

## Body
 ```html
<body class="body" xml:lang="en">
 ```
I always like to define a body class on the body element, this is because sometimes when an email renders the `<body>` element is converted to a `<div>`.  It is also useful for targeting certain email clients.

The `xml:lang="en"` sets a language for Windows Outlook, which will ingnore the other places it's set.

## Wrapping element
 ```html
<div role="article" aria-roledescription="email" aria-label="email subject line" lang="en" dir="ltr" style="font-size:medium; font-size:max(16px, 1rem)">
 ```
Inside the email body we wrap the whole content of the email in this `<div>`, I've also seen some people apply these attributes to a wrapping `<table>` personally I try and avoid tables as much as possible, but if that's your set up then you can use it on a `<table>`.

So taking a closer look at the attributes;
### `role="article"`
This is an accessibility enhancement, when navigating with a screen reader this will place the email into the landmarks menu and define the content as an article.  Although it may not be an article as such, the definition here is something that can stand alone outside the context of the rest of the page. And email fits that description.

### `aria-roledescription="email"`
As I mentioned previously, article may not be the best word to describe the content, so this will rename it to email.  This is a custom name so we can use anything here but I wouldn't advise using anything else apart from translating it to match the language of your content.  If you are unable to translate this to match your content I'd recommend leaving it off.

### `aria-label="email subject line"`
So we've said this is stand-alone content, we've said the content type is email now we give that a title.  To keep it simple I'd recommend using the subject line if you can dynamically insert that or perhaps say who the email is from "update from GoodEmailCode.com".

### `lang="en" dir="ltr"`
These are a duplication of the [lang](#lang) & [dir](#dir) set on the HTML element.  Email clients will often remove the `<html>` element so it's best to duplicate it here also.

### `font-size:medium; font-size:max(16px, 1rem)`
Some email clients may force a font-size on your email content. This resets it to be relative to the users settings so better for accessibility.

Most email clients and web browsers use a default font-size of 16px or larger but Apple mail uses a default of 12px. If you want to increase this default but still respect the the user settings then you can use `font-size:medium; font-size:max(1rem, 16px)`.  If the user has a setting smaller than 16px then the font-size will be set to 16px, if it's larger then the rem value will be used.  If `max` isn't supported then it will fallback to the previous setting of `font-size:medium;` which is the same as `font-size:1rem;` but with better support.

I've written up more about using `rem` and `em` units and how to convert your code from `px`, [Using Rem and Em units in email.](../email-accessibility/rem-and-em).


## Depreciated 

### http-equiv
**_[statcounter.com](https://gs.statcounter.com/) suggest that in October 2021 global usage of IE9 was 0.09% and WindowsPhone is 0.01%._**

 ```html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
 ```
This told the browser which version of IE to render with.  In theory this would only apply to webmail clients opening in IE 9 or below (although meta tags are likely to be stripped from webmail), emails viewed in browser in IE 9 or below and Outlook 2000-2003 for windows. 

It also enabled media queries to work on some versions of windows phone.

### supported-color-schemes

`supported-color-schemes` was renamed to `color-scheme` the old name was supported in older AppleMail version in macOS 10.14. But from macOS 10.15 onward the newer version has been supported.

### user-scalable

Previous versions of the meta viewport included `user-scalable=yes`. This allows the user to adjust the scale (pinch and zoom), however this is now default so n longer required.