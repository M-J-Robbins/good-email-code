<div class="updated">Last Updated: <time datetime="2022-01-24">24<sup>th</sup> January 2022</time></div>

# hr - The Horizontal rule
A basic horizontal rule can be done with a simple `<hr>` element.  However if you want to style it a little there are a few things to look for.

## The code
```html
<hr style="border-width: 0; background: #000; color: #000; height:1em">
```

The `<hr>` default colour is set by the border.  To simplify things and to get it to work consistently we're going to start by removing that `border-width: 0` then we need to set our custom colour using `background: #000` and to get it working in Outlook we use `color: #000`.  Because we've removed the border we now need to give it some height to see that colour showing so here I've added `height:1em`

That's it, pretty simple but there are a few other things you can add if you like.

### Width
The default is `width:100%` but you can use what suits your style.  Consider if you use a fixed width it may be good to also add a `max-width` so this stays responsive `width:500px; max-width:80%`.

Please note, Windows 10 mail has a minimum width of `4`. If a lower value is set it will default to 4.

### Margin
You can adjust the space around with a margin, either in long hand or short hand format.  However MSO Outlooks don't support left/right margin when applied directly to the `<hr>` so to get it working there we need to add the margin to a wrapping `<div>`.
```html
<div style="margin:0 20px"><hr style="margin:50px 0;border-width: 0; background: #000; color: #000; height:1em"></div>
```

Although often it may be easier to use `width` if it's a suitable alternative.

### Align
By default it will be aligned center, but with an `align=""` attribute you can set it to align left or right.


## Outlook margins
This works find in Outlook for the most part, however there is a minimum margin applied to the top and bottom.  If you need to use a small margin then you can to use a `<div>` instead.

```html
<div style="font-size:2px; line-height:2px; height:2px; margin-top: 2px; background:#000;" role="separator" >&#8202;</div>

```

Here we set the height 3 times to get support across email clients `font-size:2px; line-height:2px; height:2px;`, if the height is larger than the current font size we can leave the font-size off.

And we add `role="separator"` to add the semantic meaning of an `<hr>` if this is suitable.

## Other uses
* You could use this as a spacer if you set the colours to match the background. Although the [email spacer](../email-code/spacing) elements tend to work better.

* You can do a vertical rule, by simply setting the height larger than the width.
