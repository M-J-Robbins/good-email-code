---
layout: default
title: CTA Link 
description: A link that is styled to look like a button.
group: "code"
order: 1.6
--- 

<div class="updated">Last Updated: <time datetime="2023-04-20">20<sup>th</sup> April 2023</time></div>

# CTA Link - button

**Pedantic Semantics:**
Just a quick note to start with as I like to be a pedant, this is not a button.  Here I've named it *Link - button* as this is a link, that is styles like a button.  

Quite often in the email world we talk about buttons, when actually we mean links.  In email it's rare to use a `<button>` but really that is the only thing we should call a button and a `<a>` is a link _(or possible an anchor as that's that the `<a>` stands for)_.  When talking about design this could be referred to as a button because that's talking purely about visuals and not about function.  But as you can tell from this site, I don't know much about design, just code, so it's a link!


## The code
```html
<a href="https://parcel.io" style="background-color:#005959; text-decoration: none; padding: .5em 2em; color: #FCFDFF; display:inline-block; border-radius:.4em; mso-padding-alt:0;text-underline-color:#005959"><!--[if mso]><i style="mso-font-width:200%;mso-text-raise:100%" hidden>&emsp;</i><span style="mso-text-raise:50%;"><![endif]-->My link text<!--[if mso]></span><i style="mso-font-width:200%;" hidden>&emsp;&#8203;</i><![endif]-->
</a>
```

There is quite a lot going on in here, if you want to just copy and paste the code you can. Editing the href and the colours should be pretty self explanatory however if you want to edit the padding then best to read up about that below.


### Start with web code
  We start with a pretty standard link button that we might use on the web
  ```html
  <a href="https://example.com/" style="background-color:#005959; text-decoration: none; padding: .5em 2em; color: #FCFDFF; display:inline-block; border-radius:.4em;">
    Link Text
  </a>
  ```
  All of the styles here are optional except the `padding` and `display` without those it's a regular text link, which is also fine but that's not what we're looking at now. I've set `display` to `inline-block` so it flows with the text-align, but you could also use `block`.


### Reset padding for Outlook
  ```css
  mso-padding-alt:0;
  ```
  Because outlook doesn't respect padding very well we need to make a few changes to get this working, first up is to reset the padding using `mso-padding-alt:0`.


### Set underline colour for Windows mail
  It appears that Windows Mail doesn't respect `text-decoration: none;` or the MSO specific value of `text-underline: none` so we can't remove the underline.  We can however change the colour of it to match the background so we add `text-underline-color:#005959`.

### Add left and right padding for Outlook
  ```html
  <i style="mso-font-width:200%;mso-text-raise:100%" hidden>&emsp;</i>
  <i style="mso-font-width:200%;" hidden>&emsp;&#8203;</i>
  ```
  Inside the link either side of the text we add an `<i>` element, the element isn't relevant it's just something small and can take the style.

  This is wrapped in a conditional comment so it only shows to Outlook `<!--[if mso]> <![endif]-->`

  Inside the `<i>` we add `&emsp;`, this is an EM space. An EM space is a space, that is the width of `1em`. This is great because it's predictable and scalable. However we often want paddinng that is either more or less than `1em` so to adjust this we can use `mso-font-width` to say what persentage of `1em` we want. So for example `0.5em`=`50%` or as we have in the example code `2em`=`200%`.  There is a maximum width of `500%`, so if you need a width wider that `5em` you can add more `&emsp;` characters. 
  <!-- If for some strange reason you want to use absolute units instead of relative units. You could set `font-size` instead of `mso-font-width`. -->

  The right padding also has `&#8203;` included, this is because there needs to be a character on the other side of the space to stop it collapsing. `&#8203;` is a "Zero Width Space" so it's not going to add any extra width, it's just there to help it render.  If you are using a right-to-left language then you'll need to place the `&#8203;` in the left padding, or if you are using a lot of both left-to-right and right-to-left it might be easiest to put it in both left and right.

  T-Online will render code in MSO comments, so will end up with double padding.  We can fix this by adding a `hidden` attribute so T-Online will remove the `<i>` element but Outlook will ignore this.


### Add bottom padding
  ```html
  <span style="mso-text-raise:50%;">My link Text</span>
  ```
  Inside the link we wrap the link text with a span and apply `mso-text-raise`. Again we are going to convert our `em` units to percentage. So here we are using `0.5em` padding with will be `mso-text-raise:50%;`.


### Add top padding
  ```html
  <i style="mso-font-width:200%;mso-text-raise:100%" hidden>&emsp;</i>
  ```
  In the `<i>` we have added for either the left or right padding we add `mso-text-raise` again, but this time adding both the top and bottom padding together, this plus the height of the `&emsp;` adds to the total height of our design. So in our example we have `0.5em` + `0.5em` which equals `1em` so we add `mso-text-raise:100%`.

  If you don't have left or right padding then you'll need to add the `<i>` element to get the top padding.


## Code formatting

Be aware that additional spaces in the code can lead to extra padding width in Outlook so try and keep it all minified where possible.


## Height and width
This code uses padding to create the size of the design rather than height and width.  This is to give a more consistent rendering across email clients.  Where as most email clients will support height and width Windows Outlooks will not.

### Height
To add height just add a `height` to the `<a>` styles and for Outlook, add `line-height` of the same value to one of the `<i>` elements.

### Width
To add width just add a `width` to the `<a>` styles and for Outlook we can't do anything so you have to reply on our padding trick.  For example if you want to do `width:100%;` you'd need to estimate a padding value of what that might be for Outlook.  Be carful not to over estimate the values for Outlook as you want to avoid [text wrapping](#text-wrapping).


## Background image
Add `background-image` to the `<a>` styles.  For Outlook set a `background-color` as a fallback.


## Border radius
Add `border-radius` to the `<a>` styles.  For Outlook the corners will be square.



## Potential issues
### Text wrapping
Text will wrap normally in all clients apart from them Windows Outlooks.  As Windows Outlook is a desktop client we don't need to worry about responsive layouts, the Outlook apps will wrap as expected.  There is perhaps a usecase for a 2 line link button on desktop but I'm yet to find a way for that to work in Windows Outlook.

### mso-line-height-rule
If you are setting `mso-line-height-rule: exactly;` on a parent element that houses your link button, then you may see some issue with height in MSO Outlook. In which case try removing it or resetting it to `mso-line-height-rule: at-least`.

## `role="button"`
I've seen a few emails where a link has `role="button"` applied to it.
 
**Don't do that!**
 
As I mentioned at the top of this article, an `<a>` is a link, not a button.  For a button, we should use `<button>` (but that doesn't come up often in email).
 
Changing the semantic meaning of a link can cause some pretty serious issues.
 
Assistive technology users may not be able to find it in the links menu for the page.  And if they do find it and want to click on it, the shortcut for clicking may be different to what is expected or may not work at all.
 
So rather than helping your users click through to your side, you may be actively blocking them from doing so.

## Updates
The previouds version of this used `letter-spacing` to create the padding for Windows Outlooks, however sometime [late 2022 Cosmin noticed](https://twitter.com/M_J_Robbins/status/1575804582545960960) the Beta version of Outlook stopped supporting `letter-spacing`. I was hoping this would be fixed but then in early 2023 this came out to the production version. This lead me to finding this new way of doing it, which is actually better as it uses relative units, making it more accessible and more scalable. It's also a tiny bit less code.