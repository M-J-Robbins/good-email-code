<div class="updated">Last Updated: <time datetime="2022-02-01">1<sup>st</sup> February 2022</time></div>
# Using rem and em units in email

There are a number of different units that can be used to set sizes in CSS these can be grouped into absolute and relative.  

Absolute units don't ever change and are good for consistency but lack flexibility.  These include `px`(pixels), `pt`(points), `pc`(picas), `cm`(centimetres), `in`(inches) and more.

Relative units are more flexible as they are based of something else. These include `vw`(viewport width), `vh`(viewport height), `lh`(current line height) and more but the ones we're interested in for accessibility are `rem` and `em`.

There are also keyword values which are a bit of a mix of the relative and absolute. `medium` is the default (equal to 1rem), then `small` `large` `x-large` `xx-large` etc. are all relative to that. Then `smaller` and `larger` will adjust relative to the parent font size.

## What are EM units and REM units
`em` units are equal to the current font size, the name comes from the width of an uppercase M. So if you have a `font-size:16px` set then `1em` would be equal to `16px`. If you were then to change that to  `font-size: 20px` for a heading, `1em` would be equal to `20px`.

`rem` units are similar to `em` however these values are relative to the `:root` font size rather than the current font size so the value doesn’t change.. The name comes from Root EM.  

## Why you should be using EM and REM units

This root font size can be changed by the user, this is done in the email clients, browser or operating system preferences.  So if someone finds small text hard to read they can make it larger in the user settings and it will apply across the whole email.

This only works if we respect their settings and base our `font-size` on the `rem` set by the user.

## What is the default value of `1rem` / `medium`
In the majority of web browsers the default value is `16px` as this is a good readable font size for most people.

However, the default size in clients tends to vary a bit more. Looking at popular email clients it ranges between 12px and 17px

### Default font size for email clients
This is just to be used as a rough guide to show the range of sizes found. I have seen a few inconsistencies between tests I've run locally and via Litmus.

I'm looking at 3 factors here;
* **Default** this is taken form the user setting, equivalent to using `font-size: medium`
* **Root** this is the root font-size, mostly this woudlbe the same as the default but could be overridden by the email client style's, equivalent to using `font-size: 1rem`
* **Inherited** this is inherited from the email client styles, equivalent to adding plain text without any stylijng

| Email Client            | Default | Root | Inherited |
| ----------------------- | ------ | ------ | ------ |
| AOL                     |   16px | N/A  | 12px |
| Yahoo                   |   16px | N/A  | 13px |
| Applemail desktop       |   12px | 12px | 12px |
| Applemail iPad/iPhone   |   16px | 16px | 17px |
| IBM Notes               |   16px | 16px | 16px |
| Outlook Windows         |   18px | N/A  | 14px |
| Outlook mac             |   14px | 14px | 14px |
| Outlook Android         |   16px | 16px | 16px |
| Outlook iOS             |   16px | 16px | 16px |
| Outlook webmail and PWA |   16px | 16px | 15px |
| Outlook PWA             |   16px | 16px | 15px |
| Thunderbird             |   15px | 17px | 15px |
| Android                 |   16px | 16px | 14px |
| Gmail IMAP              |   16px | 16px | 12px |
| Gmail webmail           |   16px | 16px | 13px |
| Gmail Android           |   16px | 16px | 12px |
| Gmail iOS               |   16px | 16px | 16px |
| Samsung                 |   16px<sup>*</sup> | 16px<sup>*</sup> | 17px |
| Concast                 |   16px | 16px | 13px |
| Freenet webmail         |   16px | 16px | 16px |
| Freenet Android         |   16px | 16px | 16px |
| Freenet iOS.            |   16px | 16px | 23px |
| GMX and web.de          |   12px | N/A  | 12px |
| Mail.ru webmail         |   16px | 15px | 15px |
| Mail.ru Android         |   16px | 16px | 17px |
| Mail.ru iOS             |   16px | 16px | 15px |
| T-online                |   16px | 16px | 13px |

It’s worth noting that some of these defaults do change with the user settings already.

<sup>*</sup> Samsung sets a minimum font-size of 17px so these values of 16px only work when used to generate font-size larger of 17px or larger.

## Resetting the font-size
Unfortunately `rem` units don’t yet have full support in email clients so for now I’m recommending using `em` units inside the email. But also setting a default font-size on the parent  wrapping element to improve consistency and accessibility.

Ideally we want to return the font size to `1rem` however some email clients don’t support `rem` and in some the default value can be very small (12px in Applemail) so we will set a minimum and some fallbacks.

{% highlight html %}
<div style="font-size:medium; font-size:max(16px, 1rem)">
{% endhighlight %}

I’m going to look at these values in reverse order as that’s what the priority order is;

### `font-size:max(16px, 1rem)`
Where it’s supported this will reset the font size to user preference `1rem` with a minimum size of `16px` to adjust for small default root sizes.

The wording is confusing as we’re using `max` to set a minimum `font-size` but the idea is it’s picking the larger of the values set here.

**N.B** This will prevent the user from being able to set a smaller preferred font size.  So it’s not an ideal solution, you may want to leave this part off.

### `font-size:medium`
If the email client doesn't support `max` we will fall back to using `font-size:medium`, all email clients I've tested support this.

**Edit:** _On a previous version of this article I use `rem` units and an extra fallback to 16px `font-size:16px;font-size:1rem; font-size:max(16px, 1rem)` but later found `font-size:medium` has better support._

## Converting your code to use `em`
Mostly the standard size for `1rem` is `16px` so using that as a base will keep your sizing looking the same for most users.  So to calculate em from px, divide your `px` value by 16 and that will give you your `em` value.

So if your font is `20px` divided by 16 gives you `1.25em`.
If you font is `18px` divided by 16 give you `1.125em`
If your font is `10px` it’s too small. Don’t use 10px fonts.

Ideally your minimum font size would be `1em` but at a push I’ll sometimes go down to `.8em` if you asks really nicely and I don’t have time to talk you round.

### What styles should use `em`
So far we’ve been talking about `font-size` but you can use `em` anywhere you can use `px`.   The most important ones to consider are things that affect spacing around the text.

`line-height` is probably the most important as that should be relative to the `font-size` for that you can use `em` (also `%` works exactly the same) or unitless values are similar except they also inherit as relative, where `em` and `%` inherit as fixed value..

`margin` and `padding` around text should also be set as `em` as that can affect the readability. Elsewhere it’s not so important.

Setting `width` on text using `em` can help accessibility too.  For example `<p style="max-width:30em">` would stop small fonts creating very long paragraphs, which are harder to read.

Use `em` in media queries. If your breakpoints are defined by how the content breaks, then consider how `font-size` may affect that. Although if you are targeting devices then `px` would work better.

There’s certainly a good argument for moving everything to `em` if a user has selected a larger font then they may well want larger images, and larger layout too and it makes the design more consistent.  However there may be a reason they have chosen to change the font rather than adjusting the screen resolution or using a zoom tool.

## Inherited values
As I mentioned the value of `1em` can change through the email. This can be seen as both a pro and a con of using `em` units.

{% highlight html %}
<h1 style="font-size:2em; margin:1em 0">Heading</h1>
<p style="font-size:1em; margin:1em 0">Paragraph</p>
{% endhighlight %}

In this example if the user root font is set to 16px then the paragraph has a margin of `16px 0` but the heading is `32px 0` even though it’s the same code.  It’s likely you’d want more spacing around a heading but it can take a while to adjust to it.

Another good example if we have an email with a highlighted section where we want to increase the font-size.  We can use the same module we have for other sections but just wrap it with `font-size:1.5em` and it will increase all the sizes of that section with just a tiny bit of code.  The same could be done on a footer where we might want a small font, we can just use `font-size: 0.8em` and it will reduce the sizes of that section.

## Issues
### Attributes
`em` units don’t work inside attributes, the unit is effectively removed from the code and rendered as if no unit were used, which in defaults to `px`.

So setting `width="10em"` with render as `10px` not `10em`.  But this is a minor issue as we can set styles in the `style` attribute which does support `em`.

### VML
VML has the same issue as attributes, even if you set a size in a `style` attribute it will still render as `px`

So setting `style="width:10em"` with render as `10px` not `10em`.
