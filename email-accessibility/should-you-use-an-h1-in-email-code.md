# Should you use an `<h1>` in email code?
Short answer, yes.
Long answer...

I’m writing this following on from a couple of really interesting twitter conversation you can see here [twitter conversation 1]( https://twitter.com/Paul_Airy/status/1384824287945764866) and
[twitter conversation 2](https://twitter.com/M_J_Robbins/status/1385163970659721216)

The question is, should you use an `<h1>` in email code? It’s recommended to only have one `<h1>` on a page, however if we include one in our email code there might also be one already in the webmail.

So there are a few questions here which I’m going to try and answer...
 * [Which email clients add an `<h1>` to the content?](#which-email-clients-add-an-h1-to-the-content)
 * [Is it ok to have more than one `<h1>` on a page?](#is-it-ok-to-have-more-than-one-h1-on-a-page)
 * [Does an email count as part of the page?](#does-an-email-count-as-part-of-the-page)
 * [What benefits does an `<h1>` bring?](#what-benefits-does-an-h1-bring)
 * [What is the best option for screen reader users?](#what-is-the-best-option-for-screen-reader-users)
 * [Conclusion](#conclusion)

## Which email clients add an `<h1>` to the content?
I ran some quick tests on webmail clients and found that most webmail clients don’t add an `<h1>`
 * Gmail
 * Outlook
 * Yahoo
 * AOL
 * Freenet
 * mail.ru
 * yandex
 * rambler
But there are a few that do
 * la poste - Adds an `<h1>` to the logo
 * 163.com - Adds an `<h1>` to the logo
 * proton mail - Adds an `<h1>` to the email subject line
 * web.de - - Adds 7 `<h1>` elements in the page using sectioning layout.

_If/when I get more time I'll add to this list.  Also please let me know if you have any more email clients to add._

## Is it ok to have more than one `<h1>` on a page?
The spec says only use one `<h1>` element per page.

However when using [HTML sections and outlines](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML_sections_and_outlines) the spec says you can use one `<h1>` per section.

So problem solved? No. Unfortunately it also points out  “There are no implementations of the proposed outline algorithm in web browsers nor assistive technology”

So I think the conclusion here stays the same.  Only one `<h1>` per page is preferable.
## Does an email count as part of the page?
Most webmail clients insert the code directly into the page so this certainly counts as part of the page.  However some webmail and most apps will insert the email in an `<iframe>`.  

When using an `<iframe>` the email keeps the `<head>` and `<body>` elements so I thought it might count as a separate page, however from some testing and reading this [Accessibility Developer Guide to external content in iframes](https://www.accessibility-developer-guide.com/examples/headings/iframes/#headings-in-iframes) I found _“Screen readers integrate headings from iframes directly into the heading outline of the parent page”_.

So the answer is yes. Assistive technology generally does count email content as part of the parent page, even if it’s in an `<iframe>`.

## What benefits does an `<h1>` bring?
The main benefit is that a screen reader user can navigate directly to the `<h1>` to find the start of the main content.

If there are 2 `<h1>` elements, it might be confusing, if there is no `<h1>` it might be confusing.

## What is the best option for screen reader users?
Really this is the only important question, what is best for the users?

Doing a bit of research I found this [Webaim survey from 2017](https://webaim.org/projects/screenreadersurvey7/#heading) which asked 1792 screen reader users;

**“Which of the following page heading structures is easiest for you?”**
 * One first level heading that contains the site name - 6.6%
 * One first level heading that contains the document title - 60.0%
 * Two first level headings, one for the site name and one for the document title	33.3%

Similar results were found in the [survey from 2010](https://webaim.org/projects/screenreadersurvey3/#headings)

To me, this suggests that having the document tile as an `<h1>`’s is the most important thing. Users would rather not have the site name as an `<h1>` as well like  **la poste** and **163**  do, but we can’t control that.
## Conclusion
There are only 4 email clients I've found (so far) where this is potentially an issue and their market share is small so adding an `<h1>` would only cause an issue for a small number of users whereas leaving it off will affect more users.

Out of the 4 email clients that add `<h1>` two of them do it on the site title. The Webaim research suggests that in this case users would prefer a second `<h1>` for the document.  So adding an `<h1>` is not an issue for these email clients.

One of the email clients adds multiple `<h1>` elements anyway. Adding one more is not going to help things but I feel in this messy structure it does make sense to use `<h1>` so it stands up against the other content.  But I’m not 100% confident on that.

So one email client will benefit from not including an  `<h1>`.
One email client I’m not sure which is best, but probably best to include it.
All other email clients (I've looked at) are better off with an `<h1>`

**Use an `<h1>` in your email code.**
