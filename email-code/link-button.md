# Link - button

**Pedantic Semantics:**
Just a quick note to start with as I like to be a pedant, this is not a button.  Here I've named it *Link - button* as this is a link, that is styles like a button.  

Quite often in the email world we talk about buttons, when actually we mean links.  In email it's rare to use a `<button>` but really that is the only thing we should call a button and a `<a>` is a link _(or possible an anchor as that's that the `<a>` stands for)_.  When talking about design this could be referred to as a button because that's talking purely about visuals and not about function.  But as you can tell from this site, i don't know much about design, just code, so it's a link!


## The code
{% highlight html %}
<a href="https://example.com/" style="background: #333; border: 2px solid #f00; text-decoration: none; padding: 15px 25px; color: #fff; border-radius: 4px; display:inline-block; mso-padding-alt:0;text-underline-color:#333"><!--[if mso]><i style="letter-spacing: 25px;mso-font-width:-100%;mso-text-raise:30pt">&nbsp;</i><![endif]--><span style="mso-text-raise:15pt;">Link Text</span><!--[if mso]><i style="letter-spacing: 25px;mso-font-width:-100%">&nbsp;</i><![endif]-->
</a>
{% endhighlight %}

There is quite a lot going on in here, if you want to just copy and paste the code you can. Editing the href and the colours should be pretty self explanatory however if you want to edit the padding then best to read up about that below.


### Start with web code
  We start with a pretty standard link button that we might use on the web
  {% highlight html %}
  <a href="https://example.com/" style="background: #333; border: 2px solid #f00; text-decoration: none; padding: 15px 25px; color: #fff; border-radius: 4px; display:inline-block;">
    Link Text
  </a>
  {% endhighlight %}
  All of the styles here are optional except the `padding` and `display` without those it's a regular text link, which is also fine but that's not what we're looking at now. I've set `display` to `inline-block` so it flows with the text-align, but you could also use `block`.


### Reset padding for Outlook
  {% highlight css %}
  mso-padding-alt:0;
  {% endhighlight %}
  Because outlook doesn't respect padding very well we need to make a few changes to get this working, first up is to reset the padding using `mso-padding-alt:0`.


### Set underline colour for Windows mail
  It appears that Windows Mail doesn't respect `text-decoration: none;` or the MSO specific value of `text-underline: none` so we can't remove the underline.  We can however change the colour of it to match the background so we add `text-underline-color:#333`.

### Add left and right padding
  {% highlight html %}
  <!--[if mso]><i style="letter-spacing: 25px;mso-font-width:-100%">&nbsp;</i><![endif]-->
  {% endhighlight %}
  Inside the link either side of the text we add an `<i>` element, the element isn't relevant it's just something small and can take the style.

  This is wrapped in a conditional comment so it only shows to Outlook `<!--[if mso]> <![endif]-->`

  We add `letter-spacing:` to the amount of padding we want, and a `&nbsp;` so that spacing has something to apply to.

  By adding the `&nbsp;` we've just increased the padding a little so the value is now more than the desired amount, to remove that extra space we make the `&nbsp;` zero width by setting `mso-font-width:-100%`.


### Add bottom padding
  {% highlight html %}
  <span style="mso-text-raise:15pt;">Link Text</span>
  {% endhighlight %}
  Inside the link we wrap the link text with a span and apply `mso-text-raise` if you are designing with `px` write it as `pt` but don't adjust the value.  Not sure why but this give a more exact match to other email clients.


### Add top padding
  {% highlight html %}
  <!--[if mso]><i style="letter-spacing: 25px;mso-font-width:-100%;mso-text-raise:30pt">&nbsp;</i><![endif]-->
  {% endhighlight %}
  In the `<i>` we have added for either the left or right padding we add `mso-text-raise` again using `pt` units but this time adding both the top and bottom padding together, this plus the height of the `nbsp;` adds to the total height of our design.

  If you don't have left or right padding then you'll need to add the `<i>` element to get the top padding, keep the `mso-font-width:-100%;` but no need to include the `letter-spacing`


## Code formatting

If there is a space or new line between the conditional comment `<!--[if mso]> <![endif]-->` and the `<span> </span>` then extra padding will be added to the link button.  This could be an issue with some ESPs that will reformat your code before sending or sharing code with other developers who like to tidy code to a more readable format.


## Height and width
This code uses padding to create the size of the design rather than height and width.  This is to give a more consistent rendering across email clients.  Where as most email clients will support height and width MSO Outlook will not.

### Height
To add height just add a `height` to the `<a>` styles and for Outlook, add `line-height` of the same value to one of the `<i>` elements.

### Width
To add width just add a `width` to the `<a>` styles and for Outlook we can't do anything so you have to reply on the `letter-spacing` trick.  For example if you want to do `width:100%;` you'd need to estimate a `px` value of what that might be for Outlook.  Be carful not to over estimate the values for Outlook as you want to avoid [text wrapping](#text-wrapping).


## Background image
Add `background-image` to the `<a>` styles.  For Outlook set a `background-color` as a fallback or use a [VML button](https://buttons.cm).


## Border radius
Add `border-radius` to the `<a>` styles.  For Outlook the corners will be square or use a [VML button](https://buttons.cm).



## Potential issues
### Text wrapping
Text will wrap normally in all clients apart from MSO Outlook.  As MSO Outlook is a desktop client we don't need to worry about responsive layouts, the Outlook apps are not MSO so they wrap as expected.  There is perhaps a usecase for a 2 line link button on desktop but I'm yet to find a way for that to work in MSO Outlook.

### mso-line-height-rule
If you are setting `mso-line-height-rule: exactly;` on a parent element that houses your link button, then you may see some issue with height in MSO Outlook. In which case try removing it or resetting it to `mso-line-height-rule: at-least`.
