# Rounded corners

```
<v:shapetype id="corner" path="Ml0 1 1 1 C1 1 0 1xe" coordsize="1 1" fillcolor="#fff" stroked="f"/>

<table role="presentation" border="0" cellspacing="0" cellpadding="0" width="600" align="center" style="color:#fff;background:#000"><tr><td>
<v:shape type="#corner" style="width:30;height:30;position:absolute;left:0;flip:y;"/>
<v:shape type="#corner" style="width:30;height:30;position:absolute;flip:x y;mso-position-horizontal:right;"/>
  <div style="">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Culpa incidunt dolores officiis voluptatum vitae, rem perspiciatis, facilis delectus modi esse laudantium amet labore explicabo consectetur maiores quod molestiae! Nisi, qui. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Culpa incidunt dolores officiis voluptatum vitae, rem perspiciatis, facilis delectus modi esse laudantium amet labore explicabo consectetur maiores quod molestiae! Nisi, qui.</div>
<div style="line-height:30px;">
  <v:shape type="#corner" style="width:30;height:30;position:absolute;left:0;"/>
  <v:shape type="#corner" style="width:30;height:30;position:absolute;flip:x;mso-position-horizontal:right;"/>&nbsp;
</div>
</td></tr></table>
```


`<v:shapetype id="corner" path="Ml0 1 1 1 C1 1 0 1xe" coordsize="1 1" fillcolor="#f00" stroked="f"/>` this defines the shape, colour and stroke.  This method might not work in Windows 10, we might need to define each path.

`flip:x` can flip it to fit each corner.  Could also use `rotation:90` here.

`mso-position-horizontal:right;` aligns to the right of the container.

`width:30;height:30;` this give the size of the corner.  We can simulate 8 digit border-radius with this.

Still a few issues with it adding space.  Remove the `<p>` and the below content will wrap, but content above will not so need(`<div style="line-height:30px;">`).
