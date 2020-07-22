# Columns

Columns, laying out content beside other content, seems so simple but is one of the hardest things to achieve.  There are a number of ways of doing this but the one I find to be the most reliable and accessible is Ghost tables.

## The code
{% highlight html %}
<!--[if true]>
<table role="presentation" width="100%" style="all:unset;opacity:0;">
  <tr>
<![endif]-->
<!--[if false]></td></tr></table><![endif]-->
<div style="display:table;width:100%;">
  <!--[if true]>
    <td width="50%">
  <![endif]-->
  <!--[if !true]><!-->
    <div style="display:table-cell;width:50%">
  <!--<![endif]-->
      Column 1 content
  <!--[if true]>
    </td>
  <![endif]-->
  <!--[if !true]><!-->
    </div>
  <!--<![endif]-->
  <!--[if true]>
    <td width="50%">
  <![endif]-->
  <!--[if !true]><!-->
    <div style="display:table-cell;width:50%">
  <!--<![endif]-->
      Column 2 content
  <!--[if true]>
    </td>
  <![endif]-->
  <!--[if !true]><!-->
    </div>
  <!--<![endif]-->
</div>
<!--[if true]>
  </tr>
</table>
<![endif]-->
{% endhighlight %}

### The HTML part
If you take all the outlook code out of this it's pretty simple.
{% highlight html %}
<div style="display:table">
  <div style="display:table-cell;width:50%">
    Column 1 content
  </div>
  <div style="display:table-cell;width:50%">
    Column 2 content
  </div>
</div>
{% endhighlight %}

Here I've used `display:table` on the outer div and `display:table-cell` on the inner divs. You could also just define `display:inline-block` on the inner divs.  There are pros and cons to both approaches.

*table-cell* Can auto fill the width of any columns that don't have width defined.  A height of all columns will be determined by the height of the tallest. This does require a media query of you want the columns to stack.

*inline-block*  Can stack columns without any code in the head.  Elements that are inline-block have additional spacing added to them, this mean 2 columns set at 50% width will actually flow onto the next line.  There are fixes for this but they are delicate and can broken by email client or ESP support.  One advantage for this method is columns can stack without media queries.

### The MSO Outlook part
Again if we remove all the conditional comment and HTML code it looks much simpler
{% highlight html %}
<table role="presentation" width="100%">
  <tr>
    <td width="50%">
      Column 1 content
    </td>
    <td width="50%">
      Column 2 content
    </td>
  </tr>
</table>
{% endhighlight %}

Here we have a table with 2 columns or 50% width.

### T-online
Unfortunately T-online will render all conditional comments, so here it will show both the MSO and the HTML version.  To prevent this we first close the MSO table using `<!--[if false]></td></tr></table><![endif]-->` this conditional comment using `false` will not render for Outlook.  Depending on the styling we may still see a part of that table so we add `all:unset;opacity:0;` to the table styles.

### Additional columns
Using this method you can add as many columns as you like just repeat this part of the code as many times as you like and adjust the width values.  
{% highlight html %}
<!--[if true]>
  <td width="10%">
<![endif]-->
<!--[if !true]><!-->
  <div style="display:table-cell;width:10%">
<!--<![endif]-->
    Column 1 content
<!--[if true]>
  </td>
<![endif]-->
<!--[if !true]><!-->
  </div>
<!--<![endif]-->
{% endhighlight %}

You don't actually need to define a width, if left undefined it will be generated automatically. This can work well for a responsive layout if you want one column fixed (maybe containing an image) and one column fluid (maybe containing text).

### Responsive stacking
Columns don't work so well on small viewports so it's likely you'll want to stack them.  To do this you simply add a class to the column divs, then inside a media query you can set them to `display:block`.  Remember to use `!important` if you have inline styles set.
{% highlight css %}
.column{
  display:block !important;
  width:100% !important;
}
{% endhighlight %}

You can also reorder the content by using `display:table-header-group` on the column you want sent to the top and `display:table-footer-group` on column sent to the bottom.
*N.B We can reorder display but we can't reorder the DOM.  This means anyone using a screen reader or tabbed input will follow to flow of the code not the design on the page.  Where possible it's best to keep the order of content on the page to match the order in the code. If you still want to reorder the content then read on.*

{% highlight css %}
.column-top{
  display:table-header-group !important;
  width:100% !important;
}
.column-bottom{
  display:table-footer-group !important;
  width:100% !important;
}
{% endhighlight %}

And if you want to pull one column out and leave the others side by side you can use `display: table-caption` along with `caption-side` to place it at the top or bottom.  This only works for the first or last column.
{% highlight css %}
.column-bottom{
  width: 100% !important;
  display: table-caption !important;
  caption-side: bottom;
}
{% endhighlight %}

You can also use `display: table-caption` along with `display:table-header-group` and `display:table-footer-group` to do some complex reordering of multiple columns.  

`caption-side: top;` will sit above `display:table-header-group` and `caption-side: bottom;` will sit below `display:table-footer-group`.


<div style="display:none">
<template>
```
## Other methods
As I said in the intro, there are other ways of achieving this which may better suit your situation.

### The "th method"

### Float tables

### Float image
```
</template>
</div>
