# Text
There are a large number of elements in HTML that can be used for text, I'm going to talk about some of the basics.

## Headings and Paragraphs
{% highlight html %}
<h1 style="margin: .67em 0; font-size:2em">Heading 1</h1>
<h2 style="margin: .83em 0; font-size:1.5em">Heading 2</h2>
<h3 style="margin: 1em 0; font-size:1.17em">Heading 3</h3>
<h4 style="margin: 1.33em 0; font-size:1em">Heading 4</h4>
<h5 style="margin: 1.67em 0; font-size:.83em">Heading 5</h5>
<h6 style="margin: 2.33em 0; font-size:.67em">Heading 6</h6>
<p style="margin: 1em 0;">Paragraph</p>
{% endhighlight %}

Not much you need to do here, but I do advise setting the `margin` and `font-size` if you want consistency.  Most styles like `font-family` and `color` will inherit across all email clients for these elements so no need to reset those.  But Outlook apps, Samsung, mail.ru and Yahoo(on IE) all do some form of reset on the `margin` and/or `font-size`.

In the code sample above I've set some default styles to match typical user agent settings but please adjust these to suit your design.


## Text formatting
Some text formatting can be achieved by using HTML rather than CSS.  The advantage here is that we can add semantic meaning to the content rather than just visual styles.  There are also some styles that add no meaning, and therefore have the same affect as a styled `<span>` element.  So when adding text formatting it's important to think about if you want the semantic meaning added or if this is purely a visual style.

### Bold
{% highlight html %}
<strong>Important text</strong> <b>Bold text</b>
{% endhighlight %}
The `<strong>` element has semantic meaning, the `<b>` does not.  When testing in Litmus `<strong>` didn't always apply bold styling to the text when viewed in IE.  I'm not sure of which version this is but you may need to add `style="font-weight: bold"`.

### Italic
{% highlight html %}
<em>Emphasized text</em> <i>Italic text</i>
{% endhighlight %}
The `<em>` element has semantic meaning, the `<i>` does not.  When testing in Litmus `<em>` didn't always apply italic styling to the text when viewed in IE.  I'm not sure of which version this is but you may need to add `style="font-style: italic;"`.

### Strikethrough
{% highlight html %}
<del>Deleted text</del> <s>Incorrect text</s>
{% endhighlight %}
Both of these are semantic but with slightly different meanings.  However currently this meaning isn't passed along to the accessibility tree so you will need to find another solution to pass that information to a screen reader.  

Use `<del>` along with `<ins>` to show when text has been removed and replaced.

GMX and Web.de remove the `<s>` element along with any styles, class or id. So you may want to add `<span style="text-decoration: line-through;">` nested inside to support those clients.

MSO version of Outlook add a `color` to the `<del>` element, I've had a quick look and simply apply a `color` inline doesn't override it, so needs a little more testing.

There is also the `<strike>` element but as that is deprecated so I'm not going to cover it here.

### Underline
{% highlight html %}
<ins>Inserted text</ins> <u>Stylistically different text</u>
{% endhighlight %}
Both of these are semantic but with slightly different meanings.  However currently this meaning isn't passed along to the accessibility tree so you will need to find another solution to pass that information to a screen reader.  

Use `<ins>` along with `<del>` to show when text has been removed and replaced.

Yahoo and AOL remove the `<ins>` element along with any styles, class or id. So you may want to add `<span style="text-decoration: underline;">` nested inside to support those clients.

MSO version of Outlook add a `color` to the `<ins>` element, I've had a quick look and simply apply a `color` inline doesn't override it, so needs a little more testing.

Be carful when underlining text as this is often a visual queue for a hyperlink and may lead confuse the reader.

### Offset
{% highlight html %}
<sub>Subscript text</sub> <sup>Superscript text</sup>
{% endhighlight %}
These are purely typographic and pass no semantic meaning.

### Small
{% highlight html %}
<small>Small text</small>
{% endhighlight %}
This is purely typographic and passes no semantic meaning. It renders the text 1 font-size smaller than the current setting.




<div style="display:none">
<template>
```
https://browserdefaultstyles.com/


<br> break<br>
<a>link</a><br>

<dfn>dfn- definition</dfn>
<abbr>abbr - abbreviation</abbr>

<q cite="cite">quote</q>
<blockquote>blockquote</blockquote>
<cite>cite</cite> <br>

<code>code</code>
<pre>pre      space</pre>
<samp>samp - sample</samp> <br>
<kbd>kbd - keyboard input</kbd> <br>
<var>var - variable</var> <br>

```
</template>
</div>
