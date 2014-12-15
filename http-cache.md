## HTTP cache headers

The modern day developer has a wide variety of techniques and technologies available to improve application performance and end-user experience. One of the most frequently overlooked technologies is that of the HTTP cache.

HTTP caching occurs when the browser stores local copies of web resources for faster retrieval the next time the resource is required. As your application serves resources it can attach cache headers to the response specifying the desired cache behavior.


###HTTP cache headers**

**Cache-Control**

The Cache-Control header is the most important header to set as it effectively ‘switches on’ caching in the browser. With this header in place, and set with a value that enables caching, the browser will cache the file for as long as specified. Without this header the browser will re-request the file on each subsequent request.s


```
Cache-Control:public, max-age=31536000
```

第一个参数有public 和 private两个选项，（具体区别可以看看这个 http://stackoverflow.com/questions/3492319/private-vs-public-in-cache-control）max-age设定cache生效的时间 这里的单位是秒

**Expires**

Expires simply sets a date from which the cached resource should no longer be considered valid.

> Note: If both Expires and max-age are set max-age will take precedence.

就是一个简单的过期时间 过了这个时间 就重新获取

> Cache-Control 和 Expires 可以不和服务器端交互 只要查看本地是否有 然后 过没过期 就可以拿过来用了

```
Expires: Mon, 25 Jun 2015 21:31:12 GMT
```

While Cache-Control and Expires tells the browser when to next retrieve the resource from the network a few additional headers specify how to retrieve the resource from the network. These types of requests are known as conditional requests.

###Conditional requests

Conditional requests are those where the browser can ask the server if it has an updated copy of the resource. The browser will send some information about the cached resource it holds and the server will determine whether updated content should be returned or the browser’s copy is the most recent. In the case of the latter an HTTP status of 304 (not modified) is returned.

Though conditional requests do invoke a call across the network, unmodified resources result in an empty response body – saving the cost of transferring the resource back to the end client. The backend service is also often able to very quickly determine a resource’s last modified date without accessing the resource which itself saves non-trivial processing time.


**Time-based**

A time-based conditional request ensures that only if the requested resource has changed since the browser’s copy was cached will the contents be transferred. If the cached copy is the most up-to-date then the server returns the 304 response code.

通过	Last-Modified来确定资源最后的修改时间 访问一个资源的时候 responseHeaders里面会有这么一项

```
Last-Modified: Mon, 03 Jan 2011 17:45:57 GMT

```
记录资源的最后修改时间

下次浏览器再次访问这个资源的时候 会在requestHeaders里面添加这么一项

```
If-Modified-Since: Mon, 03 Jan 2011 17:45:57 GMT
```
如果服务器发现从这个时间起 没有变化 就会返回一个空body 并且304 response code

**Content-based**

The ETag (or Entity Tag) works in a similar way to the Last-Modified header except its value is a digest of the resources contents (for instance, an MD5 hash). This allows the server to identify if the cached 

> This tag is useful when for when the last modified date is difficult to determine.

通过Etag来访问资源 responseHeaders里面会有这么一项

```
ETag: "15f0fff99ed5aae4edffdd6496d7131f"
```

下次再请求改资源的时候 requestHeaders里面会加一项

```
If-None-Match: "15f0fff99ed5aae4edffdd6496d7131f"

```

服务器会对比两个值 如果一样 说明没有改变 返回空body 和 304 response code
