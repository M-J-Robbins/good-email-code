# CSS reset


Gmail on iOS sets the body to
body{
  -webkit-text-size-adjust: none;
  background-color: #ffffff;
  color: #313131;
  font-family: Roboto;
  font-size: 16px;
  line-height: 1.4;
  margin: 0;
  margin-right: 15px;
  padding: 0;
  word-spacing: 1px;  -  This can cause issues with the font-size:0; fix for display:inline-block; columns.
  word-wrap: break-word;
  min-height: 10px;
}


```
.wrapper{
  font-size:max(1rem, 16px);
  font-size:1rem;
  word-spacing:normal;
}
h1, h2, h3, h4, h5, h6, p{
  margin: 1em 0;
}
*{
  text-align:initial;
}
yahoo adds text-align: -webkit-match-parent; which can cause issue for rtl languages opened in ltr yahoo (and I assume the oppersite too)
```
