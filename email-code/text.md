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




<template>
```
https://browserdefaultstyles.com/


<br> break<br>
<a>link</a><br>

<strong>strong</strong> <br>
<b>b-bold</b> <br>

<em>em-emphasized</em> <br>
<i>i-italic</i> <br>

<u>u-underline</u> <br>

<s>s-strikethrough</s> <br>
<del>del-deleat</del> <br>
<ins>ins-inserted</ins> <br>

<dfn>dfn- definition</dfn>
<abbr>abbr - abbreviation</abbr>

<q cite="cite">quote</q>
<blockquote>blockquote</blockquote>
<cite>cite</cite> <br>

<sub>sub</sub> <br>
<sup>sup</sup> <br>

<code>code</code>
<pre>pre      space</pre>
<samp>samp - sample</samp> <br>
<kbd>kbd - keyboard input</kbd> <br>
<var>var - variable</var> <br>

```
</template>
