---
layout: default
title: Text In Images
description: Looking at some of the issues associated with including text in images.
group: "accessibility"
order: 3.4
--- 

<div  class="updated">Last Updated: <time  datetime="2022-02-01">1<sup>st</sup> February 2022</time></div>

# Text In Images
This is something that comes up from time to time. Is it ok to add text in images in email?

There is a bit of a misconception that all you need to do is add alt text and your code is now accessible. This is a bit of an oversimplification. Although missing (or badly written) alt text is one of the worst accessibility issues, it's not the only one.

Below I’ve listed a few [accessibility issues](#accessibility-issues) along with a few [other issues](#other-issues) that are worth considering if you are going to include text in images. This probably isn't everything, if you have any more let me know.


## Accessibility issues


### Screen readers will announce every image as an image
It’s not a big issue if it's only 1 short sentence, but it can quickly get distracting and can interrupt the flow of the content if too much of your text is in images.


### Adding semantic structure is possible but has limitations
Yes, we can still keep semantic structure by wrapping our images in HTMl.


```html
<h1>
  <img  src="heading.png"  alt="Is it ok to add text in images in email?">
</h1>
```

But this does mean separating images into individual HTML elements, heading paragraphs, list-items etc.

When using an image for a heading like this (or a link), the alt text now has an additional function it needs to perform. It is possible to do this well, but it does add an extra layer of complexity.

And although it is possible, at the time of writing, I've not seen a single example of this in a production email.  

### Text in images does not work well in reader view.
When opening in reader view you will still see the image, it doesn't pull the alt text out. The point of reader view is to remove all the distraction and make the text easier to read. So keeping the text in an image defeats the point of reader view. 

### Text readers ignore images
With a text reader, you can highlight some text and have it read out to you. This is different to a screen reader in that is doesn't have the navigation aspect or the options to interact with the content. It just reads the text. 

Generally speaking, text readers are used more by people with reading difficulties, screen readers are used more by people with visually impalements, but they do overlap.

I use a text reader occasionally when there is a word I'm struggling to read. Also, sometimes if I'm concentrating too hard on reading I struggle to take in the content.

### Users can't highlight text
This can be used, to help keep place when reading or to look up the meaning of a word. I do this quite often too.

### Text styles are not editable
There are a number of tools and browser extensions that allow a user to adjust the styling of text to make it easier for them to read. For example they may want to adjust the font, colour or size.   

These work by altering the CSS, so will only work on HTML and can't change an image.

### Text is not translatable
Translation tools typically don't look at images and won't be able to translate the content on the page.

### Viewing on small viewports
Images can scale down, but the text can’t flow to a new line. This can lead to unreadably small text on small viewports.

### Viewing with zoom or magnify tools
When the image is scaled up, the text will get blurry making it harder to read. You could use very high-res images but that causes other issues.

  

## Other issues

Accessibility is the main concern with text in images, but there are some other things to think about as well.

### Doesn’t work very well in inbox search
If a user is trying to find your email, they may do a search for some of the content they remember seeing. Some email clients will include alt text in the search and return your email, some won't. I've not done a lot of testing on this but Yahoo and AOL don't return results.

### Doesn’t work at all in find in page search
When the email is open a user might use the find function (`ctrl + f` or `cmd + f`) to look for some content. But that does not include text in images or alt text.

### Increases load time of the email
Users have short attention spans, don't make them wait.

### Potential for load error
There are a number of reasons an image might load, it's not common but it's an unnecessary risk.

### Doesn’t work offline
If there is no internet connection, there are no images. So the user can't consume your content.

### Doesn't work well when images are disabled
If images are disabled by the email client settings, there are no images. It's less likely the user will choose to download them if they can't see much other content to convince them to.

### Harder to make quick updates to copy
Changing text in code is very quick and easy, it may not even require a developer. Changing text in an image mostly requires specialist software, then it needs to be exported and optimised.

### Alt text and image text can fall out of sync
If you do make an update to an image, you must also update the alt text. This is an extra added risk that isn't needed.

## Conclusion
I'm not saying never use text in an image, you absolutely can. However, you must consider all the above points. 

To some extent, a lot of these issues could be worked around but mostly it's so much easier to just use text.