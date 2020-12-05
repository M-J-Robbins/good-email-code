# SVG

Scalable Vector Graphics or SVG, is a markup language for creating vector based images.  Because these images are created in code rather than pixels they can scale to any size without pixelating.  This is the same way fonts can look clear at any size.  And because it's code you can edit the image to change appearance to fit smaller viewports, change colours to fit with darkmode or even add hover effects.

There are 2 ways to use SVG in your email, Embedded or External.  

## Embedded SVG
This includes the code for the image inside the HTML, this means the image can still be seen even with images disabled. Also it's worth noting that this also adds to the file size of the email so including a complicated image may oush teh file size over 100kb and potentially lead to issues with sending speed, deliverability and clipping in Gmail.


### The code
{% highlight html %}
<svg width="150" height="150" role="img">
  <title>Alt text</title>
  <switch>
    <g>
      <circle cx="75" cy="75" r="75" fill="red" />
    </g>
    <foreignObject>
      <p style="font-size:50px">SVG Fallback</p>
      <img src="https://dummyimage.com/100x100/00FF00/fff&text=fallback" alt="alt text">
    </foreignObject>
  </switch>
</svg>
{% endhighlight %}

### Accessibility
To help this work with assistive technology, I've set a `role="img"` on the `<svg>` tag and included a `<title>` inside it where I have set the alt text.  If your image is purely decorative and adds no meaningful information then you can leave both of these off.

### `<switch>`
This will evaluates its direct child elements in order, and will render the first valid one it finds. The rest will then be ignored. I've added the `<g>` element to group together all the svg elements we're adding.  In this example code it's only one so it's not really needed but when doing a shape wth more then one part this is essential [MDN referance](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/switch).


### `<foreignObject>`
This is used to embed non-svg code.  In our example that means HTML  Because we're using the `<switch>` element this will be ignored if the SVG code renders.  However the content will still be downloaded, so if you have an `<img>` element in there the request to download will still be sent [MDN referance](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/foreignObject).


### Concast
Comcast will strip out the entire code block.

There is a bit of a work around here but it means putting the fallback code in twice.


{% highlight CSS %}
.before-svg + .after-svg{
  display:block !important;
}
{% endhighlight %}

{% highlight html %}
<div class="before-svg"></div>
<svg width="150" height="150" role="img">
  <title>Alt text</title>
  <switch>
    <g>
      <circle cx="75" cy="75" r="75" fill="red" />
    </g>
    <foreignObject>
      <p style="font-size:50px">SVG Fallback</p>
      <img src="https://dummyimage.com/100x100/00FF00/fff&text=fallback" alt="alt text">
    </foreignObject>
  </switch>
</svg>
<div class="after-svg" style="display:none">
  <p style="font-size:50px">SVG Fallback</p>
  <img src="https://dummyimage.com/100x100/00FF00/fff&text=fallback" alt="alt text">
</div>
{% endhighlight %}

Here we've added an element before the SVG with a class of `before-svg` this is just to help detect of the svg has been removed.  Then we duplicate our fallback code again in a div set to `<div class="after-svg" style="display:none">` so this will be hidden by default.

To show the fallback we use a CSS sibling selector to see if `before-svg` is a direct sibling of `after-svg` that looks like this `.before-svg + .after-svg` this will only be true if the `<svg>` element has been removed.

### Embedded SVG support
<iframe src="https://embed.caniemail.com/html-svg/" title="Embedded SVG support from caniemail.com"></iframe>

## External SVG
External SVG's are linked just like any other image in the `src` of an `<img>` element. However they are not supported across all email clients so we need a work around.

{% highlight html %}
<img src="/image.png" srcset="/image.svg 1x" alt="Alt text">
{% endhighlight %}

Here we are setting a safer image format (jpg, gif, png) as the default then using the `srcset` attribute to enhance it to show the SVG where that is supported. The `1x` refers to retina screens that may be 2 or 3 times the pixel density.  Setting it to `1` means this will target all devices that support the SVG image format.

`srceset` has slightly less support than just using an SVG in an `<img>` but there are 2 advantages to this technique. Firstly it's very simple with minimal code so easy to add. And secondly this will only ever download one image, either the png or the svg.  An alternate approach which I used in the past was to have 2 `<img>` elements and swap them with CSS but this means that both images are downloaded.


<!-- ## Base64 SVG -->
