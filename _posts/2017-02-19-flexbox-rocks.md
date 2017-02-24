---
layout: post
title: Flexbox rocks
category: css
tags: flexbox
---

I never truly figured out how positioning and float work, and always have an urge to smash my head to the keyboard whenever I have to use them, until I meet flexbox. Suddenly, it becomes the solution to almost everything. 

<!--more-->

Wanna try it for yourself? 

[Flexbox Froggy](http://flexboxfroggy.com/)

<amp-img width="600" height="300" layout="responsive" src="/assets/images/posts/flexbox_froggy.png"></amp-img>


### What is Flexbox? & Why Flexbox?

> The CSS3 Flexible Box, or flexbox, is a layout mode providing for the arrangement of elements on a page...
> 
> --- MDN

Yep, the layout mode! Just like the grid system we use heavily, it is a way for us to arrange the elements in the page. Unlike the grid system, flexbox calculates the size of the elements for us when using `flex` attribute. Even better, we have more control over the relative position of the elements.

With the help of flexbox, you would not need to deal with the margin, float, and positioning as much as you did, or even try to debug the headache causing by using these attributes, just like me...

### Learn Flexbox

Throughout my journey of learning flexbox, I figured out that it is very important to master the four basic concepts before replacing everything with flexbox. Otherwise, you will find yourself just as confused as you were using the positioning and float before.

<amp-img width="563" height="333" layout="responsive" src="/assets/images/posts/flex_terms.png"></amp-img>

### Parent & Children / Container & Items

First and foremost concept is parent and children (some people call it container and items). There is always a single parent, when you add the `display: flex` to the parent, all the child elements become the flex items.

Flex attributes could be categorized into two groups, one __could only be applied__ to parent element, while the one __only for__ child elements.

By giving parent certain flex attributes, it could manipulate the position of __all__ the child elements. When single child element is assigned with specific flex attributes, it could decide __its own position__ within the parent.

### Main Axis vs Cross Axis

The main axis and cross axis is defined by `flex-direction` (parent attribute). If you want to do anything related to alignments, you have to understand main axis and cross axis.

Image a Cartesian coordinate, when `flex-direction: row`, the main axis is along the x-axis, and the cross axis is the y-axis. The child elements will be laid out along the x-axis(main axis), from left to right.

In this case, if you want to center all the child elements, you could apply `justify-contents: center;`. Other options include, `flex-start`(align left), `flex-end`(align right), `space-between` and `space-around`.   

<p data-height="265" data-theme-id="0" data-slug-hash="LxKzLJ" data-default-tab="css,result" data-user="darktef" data-embed-version="2" data-pen-title="flexbox - justify_content" class="codepen">See the Pen <a href="http://codepen.io/darktef/pen/LxKzLJ/">flexbox - justify_content</a> by Lin Yang (<a href="http://codepen.io/darktef">@darktef</a>) on <a href="http://codepen.io">CodePen</a>. </p>
<script src="https://production-assets.codepen.io/assets/embed/ei.js"> </script>

To align all the child elements along the y-axis, `align-items` come in handy. Think it as `vertical-align`, the options include `flex-start`(align top), `flex-end`(align bottom), `center` (align middle), `stretch`(kind like `height: 100%;`) and `baseline`. `baseline` will align the baseline of text contained in the child elements.

If one of the child elements would like to be distinguished from other child elements, `align-self` could help, which will override the default or assigned `align-items` on parent element __only for that child element__. 

Everything above is based on `flex-direction: row`. Think about how `justify_content`, `align-items` and `align-self` will behave when `flex-direction: column`. Or even try it out by yourself with the codepen above. 

### Wrap

`flex-wrap` defines whether a new line will form when there are two many child elements. Very easy to understand, right? But it could get very tricky, when you combine with `flex-direction` and `reverse`.

<p data-height="265" data-theme-id="0" data-slug-hash="qRzPyQ" data-default-tab="css,result" data-user="darktef" data-embed-version="2" data-pen-title="flex-wrap" class="codepen">See the Pen <a href="http://codepen.io/darktef/pen/qRzPyQ/">flex-wrap</a> by Lin Yang (<a href="http://codepen.io/darktef">@darktef</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script src="https://production-assets.codepen.io/assets/embed/ei.js"> </script>


### Flex Shorthand（the three musketeers）

`flex` is a shorthand for three attributes together: `flex-grow`, `flex-shrink` and `flex-basis`, could __only be applied to__ child elements. 

`flex-grow` defines how the child elements will grow when there are extra space in the parent element. While `flex-shrink` defines how the child elements will shrink when there is no enough space in the parent element.

`flex-basis` defines the basis size of the child element before the remaining space is distributed. You could think it as the `min-width`.

It is always recommend to use `flex`, instead of using three attributes separately. 

<p data-height="265" data-theme-id="0" data-slug-hash="MpWvGZ" data-default-tab="css,result" data-user="darktef" data-embed-version="2" data-pen-title="flex" class="codepen">See the Pen <a href="http://codepen.io/darktef/pen/MpWvGZ/">flex</a> by Lin Yang (<a href="http://codepen.io/darktef">@darktef</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script src="https://production-assets.codepen.io/assets/embed/ei.js"> </script>

### [can i use flexbox?](http://caniuse.com/#search=flexbox)

<amp-img width="600" height="300" layout="responsive" src="/assets/images/posts/caniuse_flexbox.png"></amp-img>

[//]: # (### Common Applications)

### Resources

For anyone interested in learning flexbox, I recommend all three resources below:  
 
- [A Complete Guide to Flexbox - Chris Coyier (The Goto Ref!)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [What The Flexbox - Wes Bos (Free!)](https://flexbox.io/)
- [CSS Flexbox Layout - Treehouse](https://teamtreehouse.com/library/css-flexbox-layout)

If you have a treehouse account and already paid for it, go for the treehouse tutorial. The instructor illustrates really well about the parent and children concept, and helped me a lot when I started to learn flexbox. 

Wes Bos is a really great guy, he offered this 'What The Flexbox' to the community for free. His tutorial would be great for people who learn things by doing. The tutorial also contains real-life example, and clearly demonstrates to users why flexbox just make the frontend developers' lives so much easier.

A Complete Guide to Flexbox is my go-to reference for flexbox. The explanation for each attribute is short and concise, with a simple box and arrow illustration. It might be overwhelming when you first read it. However, after you grasp the basic concepts of flexbox, you will find it is super easy to use. Thanks to its two-column parent-children layout!

### Reference
1. [Using CSS FLexible Boxes - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)
2. [Flexbox - MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)
3. [Putting Flexbox into Practice - Zoe Gillenwater ](http://www.slideshare.net/zomigi/putting-flexbox-into-practice)
