# VML
Vector Markup Language (or VML), is an early language used for 2D vector images backed by Microsoft. Previously it was supported in Internet Explorer but was deprecated as of IE9. IE now supports and recommends using SVG instead.  But VML lives on in other MS Office products such as Excel, Word and the one we're interested in Outlook.

I'm going to look at 3 ways to create a VML image.

## Writing VML from scratch


## Creating VML using MS Word
It's possible to create a shape in MS Word using VML and export it.

Open a new doc, click insert/shapes and create your picture.  Then you can export it as an HTML file.

There is a lot of extra code that isn't needed here so you'll need to spend some time cleaning it up.

## Converting SVG to VML
This is my preferred method of creating VML

## Accessibility
From what I've seen VML isn't very accessible.  I believe Outlook will actually renders the VML as an image and displays it in an `<img>` element. So you can see it but you can't interact with it. T

Any links inside the VML aren't clickable for any users. But you can add an `href` to the outer element to make the whole object a link.

There is some attempt to create alt text based on any text inside but it is far from reliable, bits are missed.  However you can add an `alt` attribute to the outer element to pass alt text. 



## Resources
