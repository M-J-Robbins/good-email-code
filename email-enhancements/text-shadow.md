<div  class="updated">Last Updated: <time  datetime="2022-03-08">8<sup>th</sup> April 2022</time></div>

  

# Text Shadow

CSS is great. Adding a text shadow is easy `text-shadow: 2px 2px 0 #333;` just add horizontal offset, vertical offset, blur and colour.
 

[Support for `text-shadow` in email](https://www.caniemail.com/features/css-text-shadow/) is pretty good but it's not complete, so a lot of people avoid using it.

Then a question came up yesterday in the [EmailGeeks slack group](https://emailgeeks.slack.com/archives/C1Z733K1P/p1649262338420869) looking for _"unique solutions"_. I can't resist language like that so here's what I came up with.

## The code

```html
<h1  style="font-family:sans-serif; font-size:3em;color:#005959; mso-effects-shadow-color: #333; mso-effects-shadow-alpha: 100%; mso-effects-shadow-dpiradius: 0pt; mso-effects-shadow-dpidistance: 2pt; mso-effects-shadow-angledirection: 2700000; mso-effects-shadow-pctsx: 100%; mso-effects-shadow-pctsy: 100%;">
<div  style="max-height:0;mso-hide:all;"  aria-hidden="true">
<div  style="display:inline-block; margin-top:2px; margin-left:2px; color:#333;">
  This is my heading
</div>
</div>
<div  style="margin-right: 2px">
  This is my heading
</div>
</h1>
```

Ok it's quite a bit more code than our CSS solution `text-shadow: 2px 2px 0 #333;` but it works well

### font styles
Start by adding the basic font styles `font-family:sans-serif; font-size:3em;color:#005959;` as you would normally. 

I'm using an `<h1>` element here so swap that for the appropriate element, although I should point out it does need to be a block element and not an inline element. If you don't know the difference check out the [W3School guide to Block and Inline Elements](https://www.w3schools.com/html/html_blocks.asp). If you need it to be inline, then add `display:inline-block`.

### `mso-effect-shadow`
These styles set the text shadow for MSO Outlooks, other email client will just ignore this code, `mso-effects-shadow-color: #333; mso-effects-shadow-alpha: 100%; mso-effects-shadow-dpiradius: 0pt; mso-effects-shadow-dpidistance: 2pt; mso-effects-shadow-angledirection: 2700000; mso-effects-shadow-pctsx: 100%; mso-effects-shadow-pctsy: 100%;`

I've broken this down in more detail in my [guide to mso styles](../email-enhancements/mso-styles#mso-effects-shadow) so have a look at that for more detail.


### Shadow layer
Here we're adding the shadow for all other email clients by duplicating the text and placing it under the other text. This technique is loosely based on the [faux absolute position](../email-enhancements/faux-absolute-position) technique.

```html
<div  style="max-height:0; mso-hide:all;"  aria-hidden="true">
  <div  style="display:inline-block; margin-top:2px; margin-left:2px; color:#333;">
    This is my heading
  </div>
</div>
```

`max-height:0;` this is used to remove the vertical space, meaning this will sit under the text layer which we place after it.

`mso-hide:all;` is added to remove this from MSO Outlooks as we already have a good solution for them.  

`aria-hidden="true"` is to remove this content from assistive technology. We're adding the text twice to achieve the effect but we don't want assistive technology like a screen reader to read it twice.

Inside this we set another `<div>` which will hold out text.

`margin-top:2px; margin-left:2px;` will set the vertical and horizontal offset.

`color:#333;` this is setting the shadow colour.

### Text layer
```html
<div  style="margin-right: 2px">
  This is my heading
</div>
```

All we need to do in this section is balance out the horizontal offset, so on the shadow layer we've set 2px left margin, so here we need to mirror that with `margin-right: 2px`.

The reason we need this is to fix text wrapping. Text wraps when it hits the edge of its container, so adding a margin on one side will make the shadow layer wrap at a slightly different point to the text layer, when we balance these out then the text wrapping will match.

## Issues
This works well in most places but I have spotted a couple of small issues.


### IBM notes
Some older versions of Notes don't respect the `max-height` so you'll see the text positioned above rather than as a shadow underneath.

### Outlook 2007
This doesn't work on Outlook 2007, but seems ok on 2010 and later. So if you're using an email client 15 years out of date you might want to upgrade to one 12 years out of date.
  

## `text-shadow` support

Keep an eye on [CanIEmail](https://www.caniemail.com/features/css-text-shadow/) for the latest details on support for `text-shadow` CSS in email. Hopefully if/when that improves I can update this article.

<iframe  src="https://embed.caniemail.com/css-text-shadow/"  width="600"  height="400"  class="caniemail"  title="css-text-shadow support from caniemail.com"></iframe>