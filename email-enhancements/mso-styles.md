

# Using MSO- styles in Email
If you've been working in email dev, you may have come across `mso-` prefixed styles in the code, I mention them a few time on this site. MSO styles are styles that are specific to MSO (**M**icro**S**oft **O**ffice), some of these styles are unique to MSO but often these are repeats of standard CSS styles, in which case they can be used to provide a different value in MSO email clients.  

The MSO email clients include Outlook desktop app on Windows, and Windows Mail the rendering of these apps is based on Microsoft Word.  Other versions of Outlook, such as the Mac app, Android app, iOS app, the webmail and Progressive Web Apps (PWA) use regular HTML rendering and don't support these MSO styles.

There are a lot of MSO prefixed styles as documented in this great resource, [Stig's MSO reference page](https://stigmortenmyre.no/mso/html/concepts/ofconstyletable.htm). Stig got this recourse from Jason who shared a  [Microsoft Office HTML and XML Reference PDF](https://rodriguezcommaj.com/assets/resources/microsoft-office-html-and-xml-reference.pdf) that he in turn downloaded and decoded from this [Microsoft® Office HTML and XML Reference](https://docs.microsoft.com/en-us/previous-versions/office/developer/office2000/aa155477(v=office.10)).  This is one of the things I love about the email community, people are happy to share their findings and expand on each other's work.

Over the years, I've gone through this document and a few others and made some notes about which of these style work in Outlook and how to use them. 

There is quite a lot to cover, so I've broken it down into a few sections to hopefully make things easier to follow

* [MSO text styling](#mso-text-styling)
* [MSO advanced text styling (Word Art)](#mso-text-styling)
* [MSO box model](#mso-box-model)
more to follow...

## MSO text styling
There are a few different font types used here ascii, ansi, bidi, fareast, hansi, symbol. Depending on what language you're sending in ,you may need to adjust some of these styles accordingly (I need to do more testing around this).  For now I'm focusing on English content, so looking at ascii and ansi. 

### mso-ansi-font-size
Works in a similar way to `font-size`. Additionally, it will accept a unitless font (`mso-ansi-font-size:30`) and treat is as `30px`

```html
<p style="mso-ansi-font-size:30px">test</p>
```

### mso-ansi-font-style
Works just like `font-style` 

```html
<p style="mso-ansi-font-style:italic">test</p>
```

### mso-ansi-font-weight
Works just like `font-weight` 

```html
<p style="mso-ansi-font-weight:bold">test</p>
```

### mso-ansi-language
This can be used to define a language, Outlook will pass this value onto a `lang=""` attribute.  
```html
<p style="mso-ansi-language: es">prueba</p>
```

### mso-ascii-font-family
Works just like `font-family` 
```html
<p style="mso-ascii-font-family:Arial, sans-serif">test</p>
```
### mso-generic-font-family & mso-font-alt
These don't appear to work in the majority of places however, they can be used as part of a fallback for webfonts, [Read more about web font fallback with mso-generic-font-family on hteumeuleu.com](https://www.hteumeuleu.com/2019/today-i-learned-about-mso-generic-font-family/)

### mso-font-width
This works a bit like `transform:scaleX()` but is only applied to the text and unlike `transform` this does affect the flow of the DOM.  

It is set as a `%` where 100% is the default value.
```html
<p style="mso-font-width:50%">test</p>
```

### mso-color-alt / mso-style-textfill-fill-color
Both work just like `color` 
```html
<p style="mso-color-alt:#ff0000">test</p>
<p style="mso-style-textfill-fill-color:#ff0000">test</p>
```

### mso-line-height-alt
Works just like `line-height`. When using unitless values they need to be whole numbers and not decimals.  If you want a line height of`1.5` you can use `150%` or `1.5em`.
```html
<p style="mso-line-height-alt:150%">test</p>
```

### mso-line-height-rule
This is a modifier for `line-height`to say if the rule should be applied `exactly`or `at-least`.  It's only applies to fixed unit values like `px` and uses `at-least`as the default value. 

When using relative units like `%` this is not needed and `line-height` will work as expected.

It's only needed if you have a very small line height, set with a fixed unit.
```html
<p style="mso-line-height-alt:10px; mso-line-height-rule:exactly;">test</p>
```

### mso-style-textfill-fill-alpha
Works like `opacity` but only works on text and only accepts % values.  
```html
<p style="mso-style-textfill-fill-alpha:50%;">test</p>
```

### mso-style-textfill-type: none
Similar to `color:transparent` MSO email clients don't respect the `transparent` keyword so this can be used as a work around for that. 
```html
<p style="mso-style-textfill-type: none">test</p>
```

### mso-text-indent-alt
Works just like `text-indent` 
```html
<p style="mso-text-indent-alt:50px">test</p>
```

### mso-text-raise
Similar to `padding-bottom` but also works on inline elements.  It can also take a negative value to make it similar to `padding-top` 
```html
<p style="mso-text-raise:50px">test</p>
<p style="mso-text-raise:-50px">test</p>
```

### text-underline-color
Works just like `text-decoration-color`
```html
<p style="text-decoration:underline; text-underline-color: #FF0000">test</p>
```

## MSO advanced text styles (Word Art)
Back in the 90's if you want to create a poster for your school disco, you would do it in MS Word using Word Art.  If you're still loving this retro style then we can  recreate it in Outlook too. 

### mso-effects-shadow
Ok this is a complicated one, it's similar to `text-shadow` but works a little differently.
```html
<p style="mso-effects-shadow-color: #ff0000; mso-effects-shadow-alpha: 100%; mso-effects-shadow-dpiradius: 0pt; mso-effects-shadow-dpidistance: 10pt; mso-effects-shadow-angledirection: 5400000; mso-effects-shadow-pctsx: 100%; mso-effects-shadow-pctsy: 100%;">
  test
</p>
```
So I'll break that down
* `mso-effects-shadow-color` set the colour.
* `mso-effects-shadow-alpha` sets the opacity of the shadow.
* `mso-effects-shadow-dpiradius` sets the amount of blur on the .shadow.
* `mso-effects-shadow-dpidistance`sets the distance the shadow is away from the text.
* `mso-effects-shadow-angledirection` This sets the angle of the shadow.  The units it uses are 1/60000th of a degree, with 0 being out to the right of the text. So if you want it directly below the text, that's  a **90°** degree angle **×** **60000** = **5400000**.  
* `mso-effects-shadow-pctsx` sets the scale of the shadow on the X axis.
* `mso-effects-shadow-pctsy` sets the scale of the shadow on the Y axis.

### mso-style-textoutline
This is similar to CSS `-webkit-text-stroke` which is an experimental feature that's been sitting in the experimental box for some time.  Chris Coyier has a good [article on CSS text-stroke](https://css-tricks.com/adding-stroke-to-web-text/)

```html
<p style="font-size:50px; mso-style-textoutline-type:solid; mso-style-textoutline-fill-color:red; mso-style-textoutline-outlinestyle-dpiwidth:1pt;">test</p>
```
I'll break this down as well
* `mso-style-textoutline-type`  sets our text outline as `solid` or `gradient`.  I'm just focusing on solid for the moment.
* `mso-style-textoutline-fill-color` sets the colour of the outline.
* `mso-style-textoutline-outlinestyle-dpiwidth` sets the thickness of the outline.

Those first 3 are required, but if you want some more options...
* `mso-style-textoutline-fill-alpha` sets the opacity of the outline.
* `mso-style-textoutline-outlinestyle-dash` sets the outline style a bit like `border-style` the options are `solid` (default), 
`dotsys`, `dashsys`, `dashgel`, `dashdotgel`, `longdashgel`, `longdashdotgel`, `longdashdotdotgel`
* `mso-style-textoutline-outlinestyle-compound` is also a bit like `border-style` these options are `simple`(default), `double`, `tripple`,`thickthin`, `thinthick`.
Also take a look back at [mso-style-textfill-fill-alpha]() as that pairs well with using an outline.

### mso-style-textfill-type: gradient;
```html
<p style="mso-style-textfill-type: gradient;
mso-style-textfill-fill-gradientfill-shadetype:linear;
mso-style-textfill-fill-gradientfill-shade-linearshade-angle:
0;mso-style-textfill-fill-gradientfill-stoplist:'0 \#000000 1 100000\,50000 \#C00000 -1 100000\,100000 \#000000 1 100000'">
test
</p>
```

* `mso-style-textfill-type: gradient;` set this as a gradient fill.
* `mso-style-textfill-fill-gradientfill-shadetype: linear;` sets the type of gradient fill, options are `linear`(default)
* `mso-style-textfill-fill-gradientfill-shade-linearshade-angle: 5400000;` sets the direction of the gradient.  Again this uses units of 1/60000th of a degree, with 0 being a left to right gradient.
* `mso-style-textfill-fill-gradientfill-stoplist:"0 \#000000 1 100000\,50000 \#C00000 -1 100000\,100000 \#FFFFFF 0 0` sets the colours of the gradient as a comma separated list.  
  * Each part has a position, set in 1/1000th of a % (so that means 50000 = 50%). 
  * Then a hex colour escaped with a `\`. 
  * Then a number representing something I don't understand yet...
  * Then opacity set in 1/1000th of a %
  * Additionally we can also add `lumm=90000 lumo=3000` which I'm assuming stands for Luminance & Luminosity.

## MSO Box Model 
### mso-margin-top-alt, mso-margin-bottom-alt
Works just like `margin-top` and `margin-bottom`. But doesn't work with left, right or shorthand values.

```html
<p style="mso-margin-top-alt:1em;mso-margin-bottom-alt:1em;">test</p>
```

### mso-padding-alt
Works just like `padding`.  Also supports longhand values `mso-padding-top-alt`, `mso-padding-right-alt`, `mso-padding-bottom-alt`, `mso-padding-left-alt` 

```html
<p style="mso-margin-top-alt:1em;mso-margin-bottom-alt:1em;">test</p>
```

### mso-border-alt
Works just like `border`.  Also supports longhand values for sides `mso-border-top-alt`, `mso-border-right-alt`, `mso-border-bottom-alt`, `mso-border-left-alt` and for settings `mso-border-style-alt`, `mso-border-color-alt`, `mso-border-width-alt`

```html
<p style="mso-border-alt:4px solid green">test</p>
```

### mso-border-shadow
Similar to `box-shadow` but with less control.   This only works when a border is set, and the options are just `yes` and `no`, if yes then a black shadow will be added to the bottom right at the same width as the border.  

```html
<p style="border:solid red 8px; mso-border-shadow:yes">test</p>
```

