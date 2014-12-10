##CSS cheatsheet

* display

css中两大重要元素  一种叫做block element 一种叫inline element 分别对应着最基本的display两个属性 每个标签都有一个默认的display值
http://stackoverflow.com/questions/9189810/css-display-inline-vs-inline-block

1 display: block

block element在强制在新的一行开始 并且会伸展宽度到父元素的宽度 常见的元素有div form h1 - h6 p 等 *可以设置所有属性(width, height, margin, padding)*

2 display: inline

inline element 不会破坏现有的布局 会直接跟在当年文本流的后面 常见的元素有 a span input 等 *可以设置margin left,right和 padding left，right 不可以设置margin,padding的 top和bottom， 不可以设置width 和 height*

3 display: inline-block

在布局上表现为inline元素 不会另起新行 跟着当前文本后面 但是像block元素一样可以设置各种属性 *可以设置所有属性(width, height, margin, padding)*

兼容性:css

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

* the box model

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

* position

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


