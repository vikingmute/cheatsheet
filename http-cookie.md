##HTTP cookie cheatsheat

One of the biggest issues in the early days of the web was how to manage state. In short, the server had no way of knowing if two requests came from the same browser. 

**What is a cookie**

Quite simply, a cookie is a small text file that is stored by a browser on the user’s machine. Cookies are plain text; they contain no executable code. A web page or server instructs a browser to store this information and then send it back with each subsequent request based on a set of rules. Web servers can then use this information to identify individual users. Most sites requiring a login will typically set a cookie once your credentials have been verified, and you are then free to navigate to all parts of the site so long as that cookie is present and validated. Once again, the cookie just contains data and isn’t harmful in and of itself.

**Cookie creation**

A web server specifies a cookie to be stored by sending an HTTP header called Set-Cookie. The format of the Set-Cookie header is a string as follows (parts in square brackets are optional):
使用http的set-cookie头来设定一个cookie

```
Set-Cookie: value[; expires=date][; domain=domain][; path=path][; secure]
```

* expires 过期时间

```
Set-Cookie: name=Nicholas; expires=Sat, 02 May 2009 23:38:25 GMT

```

超过这个时间以后cookie自动删除掉

* the domain option 域名

```
Set-Cookie: name=Nicholas; domain=nczonline.net

```
Consider the case of a large network such as Yahoo! that has many sites in the form of name.yahoo.com (e.g., my.yahoo.com, finance.yahoo.com, etc.). A single cookie value can be set for all of these sites by setting the domain option to simply yahoo.com. The browser performs a tail comparison of this value and the host name to which a request is sent (meaning it starts the comparison from the end of the string) and sends the corresponding Cookie header when there’s a match.

The value set for the domain option must be part of the host name that is sending the Set-Cookie header. I couldn’t, for example, set a cookie on google.com because that would introduce a security issue. Invalid domain options are simply ignored.

* path 路径

和domain类似的东西

```
Set-Cookie: name=Nicholas; path=/blog

```

**Cookie销毁策略**

* Session cookies are removed when the session is over (browser is closed).

* Persistent cookies are removed when the expiration date and time have been reached.

* If the browser’s cookie limit is reached, then cookies will be removed to make room for the most recently created cookie. For more details, see my post on cookie restrictions.


**Cookie in javascript**

新建 存储 读取 都是用document.cookie这个属性来控制的

可以简单看看代码

http://www.quirksmode.org/js/cookies.html

**Cookie in Python & PHP**

https://docs.python.org/2/library/cookie.html

http://php.net/manual/zh/features.cookies.php

**Cookie vs Session**

Sessions are server-side files that contain user information, while Cookies are client-side files that contain user information. Sessions have a unique identifier that maps them to specific users. This identifier can be passed in the URL or saved into a session cookie.

Most modern sites use the second approach, saving the identifier in a Cookie instead of passing it in a URL (which poses a security risk). You are probably using this approach without knowing it, and by deleting the cookies you effectively erase their matching sessions as you remove the unique session identifier contained in the cookies.

最简单的典型场景 用户登陆 填写用户名 密码 调用后端接口以后 后端返回的时候 用Set-Cookie头返回一个特定的cookieId 同时在服务器端保存一个与之想对应的session 里面存着用户信息 访问其他需要权限的页面时 http请求发过来的时候 带着这个cookieId 然后用这个id来取session中想对应的内容 如果有对应值 判断用户已经登陆 如果没有 就没有登陆 所以 当你把浏览器端的cookie删除的时候 session也找不到对应值 就被看做没有登陆 session在浏览器关闭的时候被自动销毁

*Session生命周期*

If a cookie is not used to store the SID then the session will only last until the browser is closed, or the user goes to another site breaking the POST or query string transmission, or in other words, the session will last only until the user leaves the site.

**Best way to implement "Remember Me"**

关于“记住我”最好的设计方法

When the user successfully logs in with Remember Me checked, a login cookie is issued in addition to the standard session management cookie.

The login cookie contains the user's username, a series identifier, and a token. The series and token are unguessable random numbers from a suitably large space. All three are stored together in a database table.
When a non-logged-in user visits the site and presents a login cookie, the username, series, and token are looked up in the database.

If the triplet is present, the user is considered authenticated. The used token is removed from the database. A new token is generated, stored in database with the username and the same series identifier, and a new login cookie containing all three is issued to the user.

If the username and series are present but the token does not match, a theft is assumed. The user receives a strongly worded warning and all of the user's remembered sessions are deleted.
If the username and series are not present, the login cookie is ignored.



