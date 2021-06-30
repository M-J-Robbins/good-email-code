<div class="updated">Last Updated: <time datetime="2021-06-30">30<sup>th</sup> June 2021</time></div>

# Picture

The picture element allows us to define a number of different sources for an image.  This can be really useful for things like,
 * Using different image formats that aren't supported everywhere.  
 * Changing images for smaller viewports.
 * Changing images for dark mode.
 * Swapping an animated image to a static image for users who prefer reduced motion.

## The code
{% highlight html %}
<picture>
  <source srcset="webP-image.webp" type="image/webp">
  <img src="fallback-image.gif" alt="Alt Text!" style="">
</picture>
{% endhighlight %}

There are 3 main parts to the code
 * `<picture>` this acts as a wrapper to the content.
 * `<source>` this gives alternate options to use for the image `src`, we can add more than one option here if we like.
 * `<img>` this is the default image.  If none of the `<source>` elements match our needs or if `<picture>` isn't supported this acts as a standard `<img>` element.  We should add our `class` and `style` attributes here and as with any image it's important to include an `alt=""` attribute.  These attributes apply to all versions of the image.

### `<source>`
The `<source>` element is used to give other options to use for the `<img>` so we need to give some hints to say which image is the best to use.  This is done with 3 attributes `srcset` `type` and `media`.

#### srcset
This sets the alternate image src.  However as it uses `srcset` rather than `src` we can do a little more with it too and include a comma-separated list of image sources with either a width descriptor to define the source image width or a pixel density descriptor for high-DPI screens.
`<source srcset="image-300.png 300w, image-600.png 600w, image-2x.png 2x">`


#### type
This defines the image type, in the above example I'm using a webP image.  WebP is a great image format, it can do animation and has far better compression than a gif (to be fair the gif format was last updated in 1989 so it's done well to last this long).  However webP is not supported everywhere just yet, so using `type="image/webp"` we can suggest to switch to this image if it's supported, otherwise it will fallback to another `<source>` that is supported or go back to the fallback set in the `<img>`.

Here is a [list of image file types](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types)  you can reference.

#### media
This defines a media condition (similar to a media query), so you could, for example change an image on viewports less than 500px using this code.
{% highlight html %}
<picture>
  <source srcset="small-logo.png" media="(max-width: 500px)">
  <img src="big-logo.png" alt="Alt Text!" style="">
</picture>
{% endhighlight %}

But where this is really cool is you can use it for other enhancements, like dark mode.
{% highlight html %}
<picture>
  <source srcset="dark-img.png" media="(prefers-color-scheme: dark)">
  <img src="light-img.png" alt="Alt Text!" style="">
</picture>
{% endhighlight %}

And it's great for using as an accessibility enhancement for things like reduced motion.
{% highlight html %}
<picture>
  <source srcset="animation.webp"  type="image/webp" media="(prefers-reduced-motion: no-preference)">
  <source srcset="animation.gif"  type="image/gif" media="(prefers-reduced-motion: no-preference)">
  <img src="static.png" alt="Alt Text!" style="">
</picture>
{% endhighlight %}
In this example if the user has said they don't mind movement and there is support for webP they will see the `animation.webp` image.
If the user has said they don't mind movement but there isn't support for webP they will see the `animation.gif` image.
And if the user has said they don't want movement (or if `<picture>` isn't supported) they will see the `static.png` image.

## Additional support
We can add a little extra support by wrapping our picture element with a span so we can target it.
{% highlight html %}
<span class="picture-fallback">
	<picture>
		<source srcset="source-image.png">
		<img src="fallback-image.png" alt="alt text">
	</picture>
</span>
{% endhighlight %}

Then adding some CSS to show an alternate image.  
{% highlight html %}
<style>
span.picture-fallback{
  display: inline-block;
  background-image:url(css-image.png);
  background-repeat:no-repeat;
  background-size:contain;
}
span.picture-fallback img{
  opacity: 0;
}
span.picture-fallback picture img{
  opacity: 1;
}
</style>
{% endhighlight %}

Here we set the span to be `display: inline-block;` and set our new image as a `background-image`.

We then set the original image to be `opacity: 0;` I'm using this instead of `display:none` so we can use the same `height` and `width` of the original `<img>`.

Finally we put the image back if the picture tag is supported `span.picture-fallback picture img{opacity: 1;}`.

You can wrap that code inside a media query or use some CSS [email client targeting](https://howtotarget.email/) to make sure it only applies where you want it to.



## `<picture>` support
The `<picture>` element doesn't work everywhere but the fallback to the `<img>` is solid so I'd say it's pretty safe to use.  If you spot anywhere where the fallback isn't working, please let me know and I'll add a note.
<iframe src="https://embed.caniemail.com/html-picture/" width="600" height="400" class="caniemail" title="picture element support from caniemail.com"></iframe>
