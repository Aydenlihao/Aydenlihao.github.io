---
title: 你可能还不知的 CSS 好用的属性
date: 2020-05-11 17:31:18
tags:
  - HTML5
category: css
---

在这篇文章中，向你介绍了几个比较少见且好用的 CSS 属性，希望对你有所帮助

## writing-mode

<label style="background-color: #fff5f5;color:#ff502c;">writing-mode</label>属性定义了文本水平或者垂直排布以及在哪块级元素中文本的进行方向。为整个文档设置书时，应在根元素上设置它（对于 HTML 文档应该在 HTML 元素上设置）。它采用以下值之一<label style="background-color: #fff5f5;color:#ff502c;">horizontal-tb (default) | vertical-rl | vertical-lr</label>。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow); 
-webkit-background-clip: text; -webkit-text-fill-color: transparent;">horizontal-tb：</label>对于左对齐(ltr)脚本，内容从左到右水平流动。对于右对齐(rtr)脚本，内容从右到左水平流动。下一水平行位于上一行下方。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">vertical-rl：</label>对于左对齐(ltr)脚本，内容从上到下垂直流动，下一垂直行位于上一行左侧。对于右对齐(rtr)脚本，内容从下到上垂直流动，下一垂直行位于上一行右侧。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow); 
-webkit-background-clip: text; -webkit-text-fill-color: transparent;">vertical-lr：</label>对于左对齐(ltr)脚本，内容从上到下垂直流动，下一垂直行位于上一行右侧。对于右对齐(rtr)脚本，内容从上到下垂直流动，下一垂直位于上一行左侧。

```html

```

## font-variant-numeric

<label style="background-color: #fff5f5;color:#ff502c;">font-variant-numeric</label>CSS 属性控制数字，分数和序号标记的替代字形的使用。
它采用余下这些值之一：<label style="background-color: #fff5f5;color:#ff502c;">normal | ordinal | slashed-zero | lining-nums | oldstyle-nums | proportional-nums | tabular-nums | diagonal-fractions | stacked-fractions</label>
此属性对于设置数字样式很有用。根据情况，你可能希望显示老式的数字或带有斜杠的零，对于这些情况，<label style="background-color: #fff5f5;color:#ff502c;">font-variant-numeric</label>很有用。
请注意，<label style="background-color: #fff5f5;color:#ff502c;">font-variant-numeric</label>是<label style="background-color: #fff5f5;color:#ff502c;">font-feature-setting</label>组属性的一部分。

```html

```

## user-select

每当我们有不想让用户选择的文本，或者相反，如果发生了双击或上下文单击，希望选择所有文本时，<label style="background-color: #fff5f5;color:#ff502c;">user-select</label>属性将非常有用。

```html

```

## shape-outside

<label style="background-color: #fff5f5;color:#ff502c;">shape-outside</label>的 CSS 属性定义了一个可以是非矩形的形状，相邻的内联内容应该围绕该形状进行包装。默认情况下，内联内容包围其边边距框；<label style="background-color: #fff5f5;color:#ff502c;">shape-outside</label>提供了一种自定义此包装的方法，可以将文本包装在复杂对象周围而不是简单的框中。它采用与<label style="background-color: #fff5f5;color:#ff502c;">clip-path</label>相同的值。
<label style="background-color: #fff5f5;color:#ff502c;">clip-path</label>定义用户如何查看元素，<label style="background-color: #fff5f5;color:#ff502c;">shape-outside</label>定义其他 HTML 元素如何查看元素。

```html

```

## background-clip

<label style="background-color: #fff5f5;color:#ff502c;">backgroundclip</label> CSS 属性设置元素的背景是否扩展到其<label style="background-color: #fff5f5;color:#ff502c;">border</label> 、<label style="background-color: #fff5f5;color:#ff502c;">padding</label> 或<label style="background-color: #fff5f5;color:#ff502c;">content</label> 框之下

```html

```

## background-attachment

<label style="background-color: #fff5f5;color:#ff502c;">background-attachment</label>属性设置背景图像是否固定或者随着页面的其余部分滚动。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">scroll(default)：</label>背景图像会随着页面其余部分的滚动而移动。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">fixed：</label>当页面的其余部分滚动时，背景图像不会移动。
<label style="background-image: -webkit-linear-gradient(bottom, red, #fd8403, yellow);  
 -webkit-background-clip: text; -webkit-text-fill-color: transparent;">inherit：</label>规定应该从父元素继承属性设置值。

```html

```

## outline

<label style="background-color: #fff5f5;color:#ff502c;">outline</label>是绘制于元素周围的一条线，位于边框边缘的外围，可以起到突出元素的作用。<label style="background-color: #fff5f5;color:#ff502c;">outline</label>中有设置所有的轮廓属性，属性如下：outline-color、outline-style、outline-width。
outline-color：设置轮廓颜色
outline-style：设置轮廓样式
outline-width：设置轮廓的宽度

```html

```
