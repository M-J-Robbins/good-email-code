---
layout: default
title: Table layouts
description: Why you should avoid using table layouts as much as possible.
group: "accessibility"
order: 3.6
--- 

<div class="updated">Last Updated: <time datetime="2023-08-01">1<sup>st</sup> August 2023</time></div>

# Table layouts

For the majority of HTML emails, table layouts are the default way of structuring the code. A lot of emails use this approach to work around issues with Windows Outlook. However in my experience layout tables causes a lot more issues than they fix.

## Issues solved by table layouts
* Adding a width to a section in Windows Outlook.
* Adding a background to a section in Windows Outlook.
* Creating colum layouts in Windows Outlook. 

## Issues caused by table layouts
* Screen readers reading out tables.
* A number of email clients apply default styles to the content inside tables, blocking inherited styles.
  * Libaro / open exchange adding padding to `<th>` elements.
  * 
* Gmail munged tables
* [Outlook webmail auto zooming emails](https://twitter.com/M_J_Robbins/status/979390098339966983).
* [Tables don't always apply border radius](https://github.com/hteumeuleu/email-bugs/issues/98).
* [TD elements can't be set to `display: block` in Outlook](https://github.com/hteumeuleu/email-bugs/issues/78).
* [Table with a width attribute will stop Samsung showing responsive emails correctly](https://github.com/hteumeuleu/email-bugs/issues/73).
* [Apple Mail adds 1px width for an empty cells](https://github.com/hteumeuleu/email-bugs/issues/45).
* [SFR adds grey background to <a> tags inside <th> elements](https://github.com/hteumeuleu/email-bugs/issues/33).



These issues can all be solved by using a number of additional workarounds. But as they are spread across a number of email client they can be hard to test and adding these additional workarounds can lead to extra issues. 

The issues solved by table layouts are all in Windows Outlook. 