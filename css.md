##CSS cheatsheet

**display**

css中两大重要元素  一种叫做block element 一种叫inline element 分别对应着最基本的display两个属性 每个标签都有一个默认的display值
http://stackoverflow.com/questions/9189810/css-display-inline-vs-inline-block

1 display: block

block element在强制在新的一行开始 并且会伸展宽度到父元素的宽度 常见的元素有div form h1 - h6 p 等 *可以设置所有属性(width, height, margin, padding)*

2 display: inline

inline element 不会破坏现有的布局 会直接跟在当年文本流的后面 常见的元素有 a span input 等 *可以设置margin left,right和 padding left，right 不可以设置margin,padding的 top和bottom， 不可以设置width 和 height*

3 display: inline-block

在布局上表现为inline元素 不会另起新行 跟着当前文本后面 但是像block元素一样可以设置各种属性 *可以设置所有属性(width, height, margin, padding)*

*兼容性:css*

1 inline-block In IE6/IE7 

display: inline-block only works on elements that are naturally inline (such as spans).

```css
#yourDiv {
	display: inline-block;
	*display: inline;
	zoom: 1;
}
```
http://stackoverflow.com/questions/5838454/inline-block-doesnt-work-in-internet-explorer-7-6

2 inline-block之间的空隙

用这个属性 两个元素会出现几个像素的白色空隙 我常用的解决方法是把父元素font-size设为0 然后再在该元素上设置对应的font-size
```
ul {
	font-size: 0;
}
li {
	.inline-block();
	font-size: 14px;
}
```

http://css-tricks.com/fighting-the-space-between-inline-block-elements/

**the box model**

没啥可说的 在正常情况下 设置的宽高不是最终的宽高值 而应该是border + padding + width 的值，所以当设计图过来的时候 我们就要算半天 真他妈麻烦啊， 好在我们有下面的属性

1 box-sizing: border-box
用这个属性 我们就不用再计算了 设置宽高就是实际的宽高

```css
bos-sizing: border-box;
width: 200px;
height: 200px;
```
不过这个属性有兼容性的问题 假如是ie8以上 可以放心用 如果不是 呵呵。。。http://caniuse.com/#search=box-sizing

2 奇怪的兼容性问题

IE6如果在怪异模式下，他渲染box model的方法居然和border-box一样。。。太超前了一点，但是spec不是这么写的，所以他还是傻逼了，所以尽量避免怪异模式。

**position**

1 static

static is the default value. An element with position: static; is not positioned in any special way. A static element is said to be not positioned and an element with its position set to anything else is said to be positioned.


2 relative

relative behaves the same as static unless you add some extra properties.

Setting the top, right, bottom, and left properties of a relatively-positioned element will cause it to be adjusted away from its normal position. Other content will not be adjusted to fit into any gap left by the element.

会脱离当前文档流 跑出来啦 记住relative和别的元素没关系 和前面的 后面的都没关系 设置top left等值 就是在当前位置上然后偏移

3 absolute

absolute is the trickiest position value. absolute behaves like fixed except relative to the nearest positioned ancestor instead of relative to the viewport.Remember, a "positioned" element is one whose position is anything except static.

向上找 找父元素第一个不是static的元素（最后冒泡到viewport） 然后以这个元素的位置作为基准 从该处开始偏移

4 fixed 

这货第一用viewport做基准 然后就是呆在那里不动 不管页面动不动

写了个测试例子 http://jsbin.com/dekimavehi/1/edit?html,css,output

**float & clear**


1 float

不用多说 会遇到的两个问题：

* 假如有父元素 那么父元素的高度坍缩为0
* 假如后面有其他元素 那么会跟在float元素的后面

2 clear

在float元素后面清除掉浮动可以避免 上面那两个问题 

```css
/**
 * For modern browsers
 * 1. The space content is one way to avoid an Opera bug when the
 *    contenteditable attribute is included anywhere else in the document.
 *    Otherwise it causes space to appear at the top and bottom of elements
 *    that are clearfixed.
 * 2. The use of `table` rather than `block` is only necessary if using
 *    `:before` to contain the top-margins of child elements.
 */
.clearfix:before,
.clearfix:after {
  content: " ";
  display: table;
}
 
.clearfix:after {
  clear: both;
}
 /**
 * For IE 6/7 only
 * Include this rule to trigger hasLayout and contain floats.
 */

.clearfix {
  *zoom: 1;
}
```
前后面用伪类添加两个空的content 然后给后面那个添加clear:both属性 注意代码里面的注释 添加一些特别的hack

写的小例子 

http://jsbin.com/giqatujuse/1/edit?html,css,output

**CSS reset VS Normalize.css**

1 什么是CSS reset

A CSS Reset (or “Reset CSS”) is a short, often compressed (minified) set of CSS rules that resets the styling of all HTML elements to a consistent baseline.

In case you didn’t know, every browser has its own default ‘user agent’ stylesheet, that it uses to make unstyled websites appear more legible. For example, most browsers by default make links blue and visited links purple, give tables a certain amount of border and padding, apply variable font-sizes to H1, H2, H3 etc. and a certain amount of padding to almost everything. Ever wondered why Submit buttons look different in every browser?

Obviously this creates a certain amount of headaches for CSS authors, who can’t work out how to make their websites look the same in every browser. (NB: article coming soon about why this is a false notion!)

Using a CSS Reset, CSS authors can force every browser to have all its styles reset to null, thus avoiding cross-browser differences as much as possible.

2 什么是Normalize.css

Normalize.css is a small CSS file that provides better cross-browser consistency in the default styling of HTML elements. It’s a modern, HTML5-ready, alternative to the traditional CSS reset.


3 区别

http://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css

简单来说 就是reset重置了一切 各种标签都没有意义了， normalize为各种浏览器提供一套统一的 合理的 样式解决方案

http://www.cssreset.com/
https://github.com/necolas/normalize.css

还可以一说的是 小鱼的https://github.com/sofish/Typo.css  对中文排版支持的很不错

**CSS hack**

* 条件hack

if条件共包含6种选择方式：是否、大于、大于或等于、小于、小于或等于、非指定版本
是否：
指定是否IE或IE某个版本。关键字：空
大于：
选择大于指定版本的IE版本。关键字：gt（greater than）
大于或等于：
选择大于或等于指定版本的IE版本。关键字：gte（greater than or equal）
小于：
选择小于指定版本的IE版本。关键字：lt（less than）
小于或等于：
选择小于或等于指定版本的IE版本。关键字：lte（less than or equal）
非指定版本：
选择除指定版本外的所有IE版本。关键字：!

```html
<!--[if <keywords>? IE <version>?]>
HTML代码块
<![endif]-->
```

* 属性hack

这玩意儿少用一些吧 如果修ie德bug 最好用上面的条件hack

1 _：选择IE6及以下。连接线（中划线）（-）亦可使用，为了避免与某些带中划线的属性混。
2 *：选择IE7及以下。诸如：（+）与（#）之类的均可使用
3 \9：选择IE6+

```css
.test {
	color:#090\9; /* For IE8+ */
	*color:#f00;  /* For IE7 and earlier */
	_color:#ff0;  /* For IE6 and earlier */
}
```

如果你很自虐 想了解各种各样神奇的hack 请看 http://browserhacks.com/

**px vs em vs rem**

px是绝对长度,em是相对长度

em是相对长度 是相对他的父元素的比例 在现在多变的页面分辨率和各种设备的情况下 不可能所有设备都字体都使用一个字体大小 这时候em就可以大显身手

rem也是相对长度 但是他是相对于html根元素的

我们看看下面的例子 看看em的好处

* EM scales by updating one value

```css
html { font-size: 1em; }

h1 { font-size: 2.074em; }

h2 { font-size: 1.728em; }

h3 { font-size: 1.44em; }

h4 { font-size: 1.2em; }

small { font-size: 0.833em; }

.box { padding: 1.25em; }

@media screen and (min-width: 1400px) {
  html { font-size: 1.25em; }
}

```

* Or, recalculate every PX value

```css
html { font-size: 16px; }

h1 { font-size: 33px; }

h2 { font-size: 28px; }

h3 { font-size: 23px; }

h4 { font-size: 19px; }

small { font-size: 13px; }

.box { padding: 20px; }

@media screen and (min-width: 1400px) {
  html { font-size: 20px; }

  h1 { font-size: 41px; }

  h2 { font-size: 35px; }

  h3 { font-size: 29px; }

  h4 { font-size: 24px; }

  small { font-size: 17px; }

  .box { padding: 25px; }
}

```

详细的请看 https://j.eremy.net/confused-about-rem-and-em/

**CSS preprocessors**


**Icon font**

**Media query**
