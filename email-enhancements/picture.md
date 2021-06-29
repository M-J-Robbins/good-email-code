<div class="updated">Last Updated: <time datetime="2021-06-29">29<sup>th</sup> June 2021</time></div>

# Picture

The picture element allows us to define a number of differnt sources for an image.

## The code
{% highlight html %}
<picture>
  <source srcset="webP-image.webp" type="image/webp">
  <img src="fallback-image.gif" alt="Alt Text!" style="">
</picture>
{% endhighlight %}

There are 3 main parts to the code
 * `<picture>` this acts as a wrapper to the content.
 * `<source>` this gives alturnate options to use for the image and  `<img>` `src`, we can add more than one option here if we like.
 * `<img>` this is the default image.  If the none of the `<source>` elements match our needs or if `<picture>` isn't supported this acts as a standard `<img>` element.  We should add our `class` and `style` attributes here and as with any image it's important to include an `alt=""` attribute.  These attributes apply to all versions of the image.

### `<source>`
The `<source>` element is used to give other options to use for the `<img>` so we need to give some hints to say which image is the best to use.  This is done with 3 attributes `srcset` `type` and `media`.

#### srcset


#### type
This defines the image type, in the above example I'm use a webP image.  WebP is a great image format, it can do animation and has far better compression that a gif (to be fair the gif format was last updated in 1989 so it's done well to last this long).  However webP is not supported everywhere just yet, so using `type="image/webp"` we can suggest to switch to this image if it's supported, otherwise it will fallback to another `<source>` that is supported or go back to the fallback set in the `<img>`.

Here is a [list of image file types](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types)  you can referance.

#### media
This defines a media condition (similar to a media query), so you could for example change an image on viewports less than 500px using this code.
{% highlight html %}
<picture>
  <source srcset="small-logo.png" media="(max-width: 500px)">
  <img src="big-logo.png" alt="Alt Text!" style="">
</picture>
{% endhighlight %}

But where this is really cool is using it for dark mode.
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
And if the user has said they don't want movement they will see the `static.png` image.

## `<picture>` support
<iframe src="https://embed.caniemail.com/html-picture/" width="600" height="400" class="caniemail" title="picture element support from caniemail.com"></iframe>
