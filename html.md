##HTML Cheatsheet

* Doctype

Use the HTML5 DOCTYPE:
```html
<!DOCTYPE HTML>
```

Everything else is old and busted.
http://stackoverflow.com/questions/5629/any-reason-not-to-start-using-the-html-5-doctype

* 怪异模式和标准模式

When serving as text/html, all you need a doctype for is to trigger standards mode. Beyond that, the doctype does nothing as far as browsers are concerned.

However, to provide compatibility with older web pages, and to provide additional "intuitive" functionality, all browsers support an alternative "quirks mode".

怪异模式是为了旧的浏览器 在这些古董级浏览器上能更好的浏览 不写doctype或者doctype不在最前面 会引发怪异模式 他的表现如下 （包括了一些经典的ie6bug）

https://developer.mozilla.org/en-US/docs/Mozilla_Quirks_Mode_Behavior

* meta

The HTML <meta> Element represents any metadata information that cannot be represented by one of the other meta-related elements.

1 charset

This attribute declares the character encoding used of the page. It can be locally overridden using the lang attribute on any element. 
Authors are encouraged to use UTF-8.
亲 使用utf-8编码吧 全球通用偶 别再用gb2312 苦恼的处理乱码问题了

```html
<meta charset='utf-8'>
```
2 http-equiv & content

This enumerated attribute defines the pragma that can alter servers and user-agents behavior

content-language 没用了 可以直接在html标签上加lang属性
content-type 没用了 直接用charset属性
X-UA-Compatible 这个好好说说
The X-UA-Compatible meta tag allows web authors to choose what version of Internet Explorer the page should be rendered as. IE11+ have changes to these modes. See IE11 note below.

Here are your options: (我们一般直接用edge)

"IE=edge"
"IE=10"
"IE=EmulateIE10"
"IE=9"
"IE=EmulateIE9"
"IE=8"
"IE=EmulateIE8"
"IE=7"
"IE=EmulateIE7"
"IE=5"
Edge mode tells Internet Explorer to display content in the highest mode available. With Internet Explorer 9, this is equivalent to IE9 mode. If a future release of Internet Explorer supported a higher compatibility mode, pages set to edge mode would appear in the highest mode supported by that version. Those same pages would still appear in IE9 mode when viewed with Internet Explorer 9.

```html
<meta http-equiv='X-UA-Compatible' content='IE=edge'>
```

3 name & content

This attribute defines the name of a document-level metadata. 
一些有关seo的东西 author description keywords 

```html
<meta name='author' content='vikingmute'>
```

4 viewport
which gives hints about the size of the initial size of the viewport. This pragma is used by several mobile devices only.
Mobile browsers like Fennec render pages in a virtual "window" (the viewport), usually wider than the screen, so they don't need to squeeze every page layout into a tiny window (which would break many non-mobile-optimized sites). Users can pan and zoom to see different areas of the page. 最基本的viewport选项

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

width 属性决定视窗的宽度 你可以把他确定一个值 比如320 也可以直接使用device-width，根据不同的机器自动选择宽度 关于设备的宽度 可以查看这个网址  http://viewportsizes.com/
initial-scale 控制用户第一次加载进页面的zoom等级 
maximum-scale 当这个属性设置成1的时候 可以禁止用户放大页面



