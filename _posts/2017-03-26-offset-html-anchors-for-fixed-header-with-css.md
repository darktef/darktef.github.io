---
layout: post
title: Offset html anchors for fixed header with pure css
category: code
tags: css anchor_tag
---

Using Javascript is the intuition when I encountered this problem. __But should I spend that much effort for a simple and common problem__? 

<!--more-->

I found an answer on [stackoverflow](http://stackoverflow.com/questions/10732690/offsetting-an-html-anchor-to-adjust-for-fixed-header) with just pure css. Combining the top answer by Jan and css solution by Alessandro Alinone. I came up with the code &darr;: 

```html
<!-- put this just above the section you wanna go to -->
<a id='contact'></a>
<h2>Contact</h2>
```
```css
// For modern browsers, just add the CSS3 :target selector to the page. 
// This will apply to all the anchors automatically.
// ref: http://stackoverflow.com/a/21707103/6220029

:target {
  display: block;
  position: relative;
  top: -120px; 
  visibility: hidden;
}
```

By the way, when I was playing with anchor tag, I found that I have a huge misunderstanding about the limitation of anchor tag. 

I originally thought, ~~you could only use the anchor tag on the same page~~. However, it turns out not true. 

A typical scenario is the anchor tag in the header. Just by providing the absolute url of the link, the user will have no problem to navigate back to the section.

```html
<a href="/#contact">Contact</a> 
<!-- or -->
<a href="www.hello.com/home/#contact">Contact</a>
<!-- instead of  -->
<a href="#contact">Contact</a>
<!-- which could only locate the id of section on the same page -->
  ```