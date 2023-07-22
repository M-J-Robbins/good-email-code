---
layout: default
title: Container
description: Basic text elements.
group: "code"
order: 1.5
--- 

<div class="updated">Last Updated: <time datetime="2022-03-10">10<sup>th</sup> March 2022</time></div>

# Text
There are a large number of elements in HTML that can be used for text, I'm going to talk about some of the basics.

## Headings and Paragraphs
```html
<h1 style="margin: .67em 0; font-size:2em">Heading 1</h1>
<h2 style="margin: .83em 0; font-size:1.5em">Heading 2</h2>
<h3 style="margin: 1em 0; font-size:1.17em">Heading 3</h3>
<h4 style="margin: 1.33em 0; font-size:1em">Heading 4</h4>
<h5 style="margin: 1.67em 0; font-size:.83em">Heading 5</h5>
<h6 style="margin: 2.33em 0; font-size:.67em">Heading 6</h6>
<p style="margin: 1em 0;">Paragraph</p>
```

Not much you need to do here, but I do advise setting the `margin` and `font-size` if you want consistency.  Most styles like `font-family` and `color` will inherit across all email clients for these elements so no need to reset those.  But Outlook apps, Samsung, mail.ru and Yahoo(on IE) all do some form of reset on the `margin` and/or `font-size`.

In the code sample above I've set some default styles to match typical user agent settings but please adjust these to suit your design.


## Text formatting
Some text formatting can be achieved by using HTML rather than CSS.  The advantage here is that we can add semantic meaning to the content rather than just visual styles.  There are also some styles that add no meaning, and therefore have the same affect as a styled `<span>` element.  So when adding text formatting it's important to think about if you want the semantic meaning added or if this is purely a visual style.

### Bold
```html
<strong>Important text</strong> <b>Bold text</b>
```
The `<strong>` element has semantic meaning, the `<b>` does not.  When testing in Litmus `<strong>` didn't always apply bold styling to the text when viewed in IE.  I'm not sure of which version this is but you may need to add `style="font-weight: bold"`.

### Italic
```html
<em>Emphasized text</em> <i>Italic text</i>
```
The `<em>` element has semantic meaning, the `<i>` does not.  When testing in Litmus `<em>` didn't always apply italic styling to the text when viewed in IE.  I'm not sure of which version this is but you may need to add `style="font-style: italic;"`.

### Strikethrough
```html
<del>Deleted text</del> <s>Incorrect text</s>
```
Both of these are semantic but with slightly different meanings.  However currently this meaning isn't passed along to the accessibility tree so you will need to find another solution to pass that information to a screen reader.  

Use `<del>` along with `<ins>` to show when text has been removed and replaced.

GMX and Web.de remove the `<s>` element along with any styles, class or id. So you may want to add `<span style="text-decoration: line-through;">` nested inside to support those clients.

MSO version of Outlook add a `color` to the `<del>` element, I've had a quick look and simply apply a `color` inline doesn't override it, so needs a little more testing.

There is also the `<strike>` element but as that is deprecated so I'm not going to cover it here.

### Underline
```html
<ins>Inserted text</ins> <u>Stylistically different text</u>
```
Both of these are semantic but with slightly different meanings.  However currently this meaning isn't passed along to the accessibility tree so you will need to find another solution to pass that information to a screen reader.  

Use `<ins>` along with `<del>` to show when text has been removed and replaced.

Yahoo and AOL remove the `<ins>` element along with any styles, class or id. So you may want to add `<span style="text-decoration: underline;">` nested inside to support those clients.

MSO version of Outlook add a `color` to the `<ins>` element, I've had a quick look and simply apply a `color` inline doesn't override it, so needs a little more testing.

Be carful when underlining text as this is often a visual queue for a hyperlink and may confuse the reader.

### Offset
```html
<sub>Subscript text</sub> <sup>Superscript text</sup>
```
These are purely typographic and pass no semantic meaning.

### Small
```html
<small>Small text</small>
```
This is purely typographic and passes no semantic meaning. It renders the text 1 font-size smaller than the current setting.


## Code
```html
<p>Use an HTML5 <code style="color:red;background-color: #eee;font-family: courier, monospace;">&lt;!DOCTYPE html&gt;</code> in your email</p>
```

This is used for defining an inline sample of code. Which I do on this site often and looks like `<code>`


## Pre
This is used to preserve spaces, line breaks and tabs in the text. So how you format the code in the HTML file is how it will look on the screen. 

```html
<pre>pre      space</pre>
```

Will render all of the spaces between the words.

This is often used with `<code>` to show a multi line code sample with indentation.

Generally I'd advise setting `white-space: pre-wrap;` to allow the content to wrap on smaller viewports when using `<pre>`.

```html
<pre style="background-color: #272822; padding: 1em;white-space: pre-wrap; font-family: monospace;color: #fff;border-radius: .5em;border: 1px solid #005959;line-height: 1.3;tab-size: 2;"><code style="font-family: 'Source Code Pro', courier,monospace;"><span style="color: #97937c;">&lt;!DOCTYPE html&gt;</span>
<span style="color: #f92672;">&lt;html</span> <span style="color: #a6e22e;">lang=</span><span style="color: #e6db74;">"en"</span> <span style="color: #a6e22e;">dir=</span><span style="color: #e6db74;">"ltr"</span><span style="color: #f92672;">&gt;</span>
  <span style="color: #f92672;">&lt;head&gt;</span>
  <span style="color: #f92672;">&lt;/head&gt;</span>
  <span style="color: #f92672;">&lt;body</span> <span style="color: #a6e22e;">class=</span><span style="color: #e6db74;">"body"</span><span style="color: #f92672;">&gt;</span>
    <span style="color: #b7b39f;">&lt;!-- email content in here --&gt;</span>
  <span style="color: #f92672;">&lt;/body&gt;</span>
<span style="color: #f92672;">&lt;/html&gt;</span>
</code></pre>
```

In this example I've also done syntax highlighting to make the code easier to read.  There are a few online tools avalible that can help with that such as [highlight.hohli.com](https://highlight.hohli.com/index.php)

<br><br>


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

<mark>mark</mark>

<samp>samp - sample</samp> <br>
<kbd>kbd - keyboard input</kbd> <br>
<var>var - variable</var> <br>

```
</template>
</div>
