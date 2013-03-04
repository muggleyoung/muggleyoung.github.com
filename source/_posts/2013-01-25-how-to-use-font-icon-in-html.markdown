---
layout: post
title: "How to use font icon in HTML"
date: 2013-01-25 18:25
comments: true
categories: html css
---
##### Why Icon Fonts (图标字体) are awesome?
We can easily change the style (e.g. scale, color, shadow, opacity, rotate, etc.)

It is 100% accessible, we don't need to use image sprites then


##### Some of Icon Fonts websites:
* [Fontello](http://fontello.com/)
* [Font Awesome](http://fortawesome.github.com/Font-Awesome/)
* [fico](http://fico.lensco.be/)
* [IcoMoon](http://icomoon.io/#home)

##### Building your Icon Fonts

###### 1. Download icon fonts

I used [Fontello](http://fontello.com/) to get my Icon Fonts.

1. Go to [Fontello](http://fontello.com/)
2. Choose icons you want
3. Download webfont

Then you'll get fonts files like: \*.eot, \*.svg, \*.ttf, \*.woff.

###### 2. HTML

```
 <ul>
      <li class="icon-pencil">{date}</li>  
 </ul>
```

###### 3. CSS

Open your fontello folder, you'll see a file named "fontello.css", copy content of this css to your css file:

```
@charset "UTF-8";
@font-face {
  font-family: 'fontello';
  src: url("../font/fontello.eot");
  src: url("../font/fontello.eot?#iefix") format('embedded-opentype'), 
       url("../font/fontello.woff") format('woff'), 
       url("../font/fontello.ttf") format('truetype'), 
       url("../font/fontello.svg#fontello") format('svg');
  font-weight: normal;
  font-style: normal;
}
[class^="icon-"]:before,
[class*=" icon-"]:before {
  font-family: 'fontello';
  font-style: normal;
  font-weight: normal;
  speak: none;
  display: inline-block;
  text-decoration: inherit;
  width: 1em;
  margin-right: 0.2em;
  text-align: center;
  opacity: 0.8;
/* fix buttons height, for twitter bootstrap */
  line-height: 1em;
/* Animation center compensation - magrins should be symmetric */
/* remove if not needed */
  margin-left: 0.2em;
/* you can be more comfortable with increased icons size */
/* font-size: 120%; */
/* Uncomment for 3D effect */
/* text-shadow: 1px 1px 1px rgba(127, 127, 127, 0.3); */
}

.icon-pencil:before { content: '\270e'; } /* '✎' */
.icon-feather:before { content: '\2712'; } /* '✒' */
.icon-tag:before { content: '\e70c'; } /* '' */
.icon-comment:before { content: '\e718'; } /* '' */
```

Then you can customize the style as what you want.

DO NOT forget to include your css file in the html. I made this mistake twice, shame :(

__Done__