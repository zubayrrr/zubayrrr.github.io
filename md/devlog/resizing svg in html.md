---
created: 1652622339676
desc: ''
id: ou4gmackfon8ce8lhng8nk1
title: Resizing SVG in html
updated: 1652622339676
---
   
Open your `.svg` file with a text editor (it's just XML), and look for something like this at the top:   
   
```xml
<svg ... width="50px" height="50px"...
```
   
   
Erase width and height attributes; the defaults are 100%, so it should stretch to whatever the container allows it.   
   
   
   
---   
   
I have found it best to add `viewBox` and `preserveAspectRatio` attributes to my SVGs. The viewbox should describe the full width and height of the SVG in the form `0 0 w h`:   
   
```xml
<svg preserveAspectRatio="xMidYMid meet" viewBox="0 0 700 550"></svg>
```
   
   
   
   
---   
   
Use the following code:   
   
```xml
<g transform="scale(0.1)">
...
</g>
```
   
   
[Resizing SVG in html? - Stack Overflow](https://stackoverflow.com/questions/3120739/resizing-svg-in-html)