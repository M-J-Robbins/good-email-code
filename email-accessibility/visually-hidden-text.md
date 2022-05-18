<div class="updated">Last Updated: <time datetime="2022-05-19">19<sup>th</sup> May 2022</time></div>

# Visually hidden text

I've been playing around with this for a few years, I've had a lot of different solutions but all had issues so I wasn't ready to share them.  Finally, I think I might have it.

Doing this on the web is tricky, so doing it in email is even more complicated. Kitty Giraudel has done a lot of great work on this, so check out their articles on [CSS hide and seek](https://kittygiraudel.com/2016/10/13/css-hide-and-seek/) & [hiding content responsibly](https://kittygiraudel.com/2021/02/17/hiding-content-responsibly/). Also check out [WebAim invisible content](https://webaim.org/techniques/css/invisiblecontent/). I've read these a lot when looking for a solution to work in email.

## What is visually hidden text?
Visually hidden text is text, that is hidden, visually.  So that means the text is present, it's in the email, it is in the DOM and the accessibility tree, however, it's not visible on the screen. 

So what's the point? We can use visually hidden text to give extra information to assistive technology like screen readers that isn't shown on the screen.

For example, if we have a link with the text "Find Out More" that's not great for accessibility, it doesn't give any information, find out more about what?  If we're looking on the screen, we might see something next to it that give us context, but if we're using a screen read and especially if we're using the links shortcut menu, we don't have that context. 

So what we can do is add some visually hidden text, on screen the user will see "Find out more" but a screen reader will read "Find out more about visually hidden text".


## The code
```html
<span style="display:inline-block; max-height:0; max-width:0;mso-font-width:0%;mso-style-textfill-type: none; white-space: nowrap;">
  <span style="max-height:1px; max-width:1px; display:inline-block; overflow:hidden; font-size:1px;color:rgba(0,0,0,0);text-indent:9px;">
    hidden text
  </span>
</span>
```
Yeah, that's quite a lot of code, I'm hoping to reduce it, if I can.

### `<span>` `<span>`
I'm using 2 `<span>` elements, one to take away the space that the text adds and one to hide the text. Separating this out is the big break through I had

I'm using `<span>` elements as they are semantically neutral (don't add any meaning to the code) and Outlook won't allow  a block element like a `<div>` inside an inline element like an `<a>`.

### Removing the space
We want to remove any extra space that the text adds, so visually there is no difference. For this we add `display:inline-block; max-height:0; max-width:0;`.
Using `max-` for `height` and `width` works around Yahoo/AOL issues where `height` is converted to `min-height`.

This is the same concept as we use in the [faux absolute position](email-enhancements/faux-absolute-position).

### Windows Outlook 
The MSO Windows Outlook doesn't like any of this, however we can use some [MSO styles](email-enhancements/mso-styles) to fix it.

`mso-font-width:0%;` removes horizontal size from Outlook, and squashes the text down to take up no space.

`mso-style-textfill-type: none` makes the text transparent.

I've also added `font-size:1px;` in the inner section to help remove the vertical space in Outlook.

### White space
This is an issue I've not been able to replicate but J. Renée Beach warned [Beware smushed off-screen accessible text](https://medium.com/@jessebeach/beware-smushed-off-screen-accessible-text-5952a4c2cbfe), saying when the text is all _'smushed'_ together a screen reader may read it without the spaces, adding `white-space: nowrap;`fixes this.

Also, I noticed in a different version of the code, this helps remove vertical spacing. So I think it's good to add in.

### Hiding the text
We can hide the text in a similar way to what we've used on the outer element `display:inline-block; max-height:1px; max-width:1px; overflow:hidden;` however here we're   adding `overflow: hidden` this hides the text that as it overflows from the box. 

Also we're using `1px` rather than `0`. When something is set to `0` height and width and `overflow:hidden` then it has no size and no visibility, so it may be removed from the DOM and it won't be picked up by assistive technology.

Separating this out into these 2 parts is what makes this work.

### GANGA
GANGA (Gmail app not Gmail account) also referred to as Gmail IMAP. Doesn't support `overflow:hidden` so this means our text is still visible.

So what we can do is make the text very small with `font-size:1px;` then make it transparent using `color:rgba(0,0,0,0);`.

### Extra safe
I've not seen it, but there is a chance that in this 1px square we've created we might see a corner of a letter where the `color:rgba(0,0,0,0)` isn's supported, to protect from that happening we can push the text over a little using `text-indent:9px;`.


## Hiding things other than text
I've only focused my testing on text as that's the main use case here.  This technique should work for most inline elements

## Version2
I'm working on a smaller version, this puts everything on a single `<span>` and drops the `overflow:hidden`but otherwise the code is pretty much the same.
```html
<span style="max-height:0;max-width:0;display:inline-block;mso-font-width:0%;mso-style-textfill-type: none; white-space: nowrap;font-size:1px;color:rgba(0,0,0,0);text-indent:9px;">
	hidden text
</span>
```
Currently, I'm having issues with this version
* Text is visible on IBM notes and it's adding space.
* Samsung adds vertical spacing because it removes `white-space: nowrap`

