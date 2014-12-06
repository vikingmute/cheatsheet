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

兼容性:
1 inline-block In IE6/IE7, display: inline-block only works on elements that are naturally inline (such as spans).
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