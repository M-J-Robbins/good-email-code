<div class="updated">Last Updated: <time datetime="2021-12-17">3<sup>rd</sup> January 2022</time></div>

# ARIA landmarks in Email

ARIA landmarks are used to identify the organization and structure of an HTML document.  Assistive technology (like screen readers) can use these landmarks to help navigate a page.

A user can pull up a list of all the available landmarks and jump straight into the content they want to consume. Similar to how some users might take visual cues to quickly find the main content, or the navigation bar etc. This is way easier than reading line by line until you find what you want. 

The [2021 WebAim screen reader survey](https://webaim.org/projects/screenreadersurvey9/#landmarks) asked users how often they use landmarks to navigate an page.  Although they found these are not the primary navigation method used (heading win by a mile), over 75% of users asked do use them to some extent.


## Which landmarks are ok to use in email
There are a number of different landmarks available to us. I'm going to cover a few and heavily reference the [W3 ARIA Landmarks example](https://www.w3.org/TR/2019/NOTE-wai-aria-practices-1.1-20190814/examples/landmarks/) and the [W3C Recommendation for ARIA](https://www.w3.org/TR/wai-aria-1.1) documents as I do it.

### ✔ Article `<article>`
[W3C Recommendation for article](https://www.w3.org/TR/wai-aria-1.1/#article) describes it as

> “A section of a page that consists of a composition that forms an independent part of a document, page, or site.”


That description sounds like an email to me. As an email is completely independent of the parent document (the email client).

This is why I recommended that the entire content of the email is wrapped in an article landmark in my [email template guide](../email-code/template#wrapping-element). To make sure it's included in the landmarks menu, you need to include a label.

See the [how to include landmarks in email](#how-to-include-landmarks-in-email) section below to learn how best to implement this.

### ✔ Region `<section>`
[W3C Recommendation for region](https://www.w3.org/TR/wai-aria-1.1/#region) describes it as

> "A perceivable section containing content that is relevant to a specific, author-specified purpose and sufficiently important that users will likely want to be able to navigate to the section easily and to have it listed in a summary of the page."

It's tempting to overuse this, but be sparing with it. You don't want to flood the landmarks menu with too much content as it waters down the important stuff.  

Most emails probably don't need it, but if there is a particular part of your email you want to call out, use it for that.

Similar to an article a region requires a label in order to show up in the landmarks menu.


### ✔ Navigation `<nav>`
[W3C Recommendation for navigation](https://www.w3.org/TR/wai-aria-1.1/#navigation)
> A collection of navigational elements (usually links) for navigating the document or related documents.

Navigation doesn't require a label, but as it’s likely a webmail page may already have a navigation landmark you want to make sure you label yours to avoid confusing the user.


## Which landmarks are not ok to use in email

### ✖ Banner `<header>`
[W3C Recommendation for banner](https://www.w3.org/TR/wai-aria-1.1/#banner)
> “A region that contains mostly site-oriented content, rather than page-specific content.” 

From this description, users will be expecting the banner to be relative to the email client rather than the email, so it doesn't make much sense for us to use it in email.

> "Each page may have one banner landmark."

As it’s likely a webmail page may already have a banner landmark, it’s advised to not include a second one in the email.

Theoretically it is possible to include a `<header>` as long as it's inside another landmark as this should remove the role of `banner`. But seeing as support for `<header>` isn't great in email and the semantic meaning is removed when using it like this there no benefit to using it here.

### ✖ Contentinfo `<footer>`
[W3C Recommendation for contentinfo](https://www.w3.org/TR/wai-aria-1.1/#contentinfo)

> A large perceivable region that contains information about the parent document.

Again this suggests it's more relevant to the email client rather than the email.

> “Each page may have one contentinfo landmark.”

As it’s likely a webmail page may already have a contentinfo landmark, it’s advised to not include a second one in the email.

Theoretically it is possible to include a `<footer>` as long as it's inside another landmark as this should remove the role of `contentinfo`. But seeing as support for `<footer>` isn't great in email and the semantic meaning is removed when using it like this there no benefit to using it here.

### ✖ Main `<main>`
[W3C Recommendation for main](https://www.w3.org/TR/wai-aria-1.1/#main)

>"The main content of a document."

As much as we might like to think our email is the main content it's only one small part. Users navigating to the main section are most lily looking for their inbox.

> “Each page should have one main landmark.”

As it’s likely a webmail page may already have a main landmark, it’s advised to not include a second one in the email.

### ✖ Complementary `<aside>`

> “Complementary landmarks should be top level landmarks (e.g. not contained within any other landmarks).”

As it’s likely a webmail page may have a landmark wrapping the section when the email is, it’s advised to not to include a nested one in the email.

## How to include landmarks in email
Some good news and bad news here.  Unfortunately we can't reliably use HTML5 semantic tags for the moment, a number of email clients will remove the tag along with any attributes they have on them.  This means, no `class` no `style` etc. 

<iframe src="https://embed.caniemail.com/html-semantics/" width="600" height="400" class="caniemail" title="picture element support from caniemail.com"></iframe>

But the good news is we can use their `role` equivalents instead.  This means using a `<div>` element, then adding a `role=""` attribute on it to change it's semantic meaning.

I recommend using a `<div>` (or maybe a `<span>`) over any other element as it is a semantically neutral element, so there is no chance of clashing roles.  Also [role attributes don't work everywhere yet](https://www.caniemail.com/features/html-role/) and a `<div>` will fallback to having no meaning rather than fallback to have the wrong meaning.

So instead of using 
```html
<article>
    Content
</article>
```

we can use

```html
<div role="article">
    Content
</div>
```

Here's a list of HTML5 semantic elements and their role equivalents to help you out.

| HTML5     | Role          |
|-----------|---------------|
|`<article>`| Article       |
|`<section>`| Region        |
|`<nav>`    | Navigation    |
|`<header>` | Banner        |
|`<footer>` | Contentinfo   |
|`<main>`   | Main          |
|`<aside>`  | Complementary |


### Adding a label
In email all landmarks should have a label, to do this add a `aria-label` attribute on the landmark.

```html
<div role="navigation" aria-label="MyBrand email">
```

This will be read out as _"MyBrand email navigation"_ which helps to distinguish from the email client navigation, so the users knows what they are getting.

#### `aria-labelledby`
It is also possible to set a label by using the `aria-labelledby` attribute. however, I don't reccomend this for email.

`aria-labelledby` is a "Relationship Attribute" this means it reference an `id` attribute applied to another element to get it's content. This is great for web however, a number of email clients including Yahoo, AOL, Outlook.com, will prefix the `id` value, meaning the label no longer matches and won’t be properly connected to the landmark. 

So for example, this code where we can see the `aria-labelledby` matches the `id`.
```html
<div role="article" aria-labelledby="MyHeading">
    <h1 id="MyHeading">This is my email</h1>
</div>
```
Would become something like this and the `id` no longer matches the `aria-labelledby` so the article is left unlabelled.
```html
<div role="article" aria-labelledby="MyHeading">
    <h1 id="yiv123456789MyHeading">This is my email</h1>
</div>
```