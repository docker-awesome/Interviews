# Interviews

`Common front-end interview questions.`

## JavaScript Basic

- Cookie, localStorage, sessionStorage 区别

  `生命周期：`

  ```text
  Cookie:
    由 HTTP 协议生成，Expires属性指定一个具体的到期时间，到了指定时间以后，浏览器就不再保留这个 Cookie。
    如果不设置该属性，或者设为null，Cookie 只在当前会话（session）有效，浏览器窗口一旦关闭，当前 Session 结束，该 Cookie 就会被删除。

  localStorage：
    保存的数据长期存在，下一次访问该网站的时候，网页可以直接读取以前保存的数据。

  sessionStorage：
    保存的数据用于浏览器的一次会话（session），当会话结束（通常是窗口关闭），数据被清空；
  ```

  `存储空间：`

  ```text
  Cookie:
    单个域名设置的 Cookie 不应超过30个，每个 Cookie 的大小不能超过4KB。超过限制以后，Cookie 将被忽略，不会被设置。

  localStorage：
  sessionStorage：
    每个域名的存储上限视浏览器而定，Chrome 是 2.5MB，Firefox 和 Opera 是 5MB，IE 是 10MB。
    其中，Firefox 的存储空间由一级域名决定，而其他浏览器没有这个限制。
  ```

  `同源策略：`

  ```text
  Cookie:
    只有同源的网页才能共享, 浏览器允许通过设置相同的document.domain共享 Cookie。
    (浏览器通过document.domain属性来检查是否同源。)

  localStorage：
  sessionStorage：
    与 Cookie 一样，它们也受同域限制。只有同域下的网页才能读取。
  ```

  `通信：`

  ```text
  Cookie:
    浏览器向服务器发送 HTTP 请求时，每个请求都会带上相应的 Cookie。
  ```

  `事件：`

  ```text
  localStorage：
  sessionStorage：
    Storage 接口储存的数据发生变化时，会触发 storage 事件
  ```

  `缺点：`

  ```text
  Cookie:
    容量很小（4KB），缺乏数据操作接口，而且会影响性能
  ```

- 同源政策（“同源”指的是”三个相同“：`协议相同`， `域名相同`， `端口相同`）

  `非同源，共有三种行为受到限制:`

  ```text
  （1）无法读取非同源网页的 Cookie、LocalStorage 和 IndexedDB。

  （2）无法接触非同源网页的 DOM。

  （3）无法向非同源地址发送 AJAX 请求（可以发送，但浏览器会拒绝接受响应）。
  ```

  `对于完全不同源的网站，目前有两种方法，可以解决跨域窗口的通信问题:`

  ```text
  （1）片段识别符（fragment identifier）: 指的是，URL 的#号后面的部分 -> 父窗口把所要传递的信息，写入 iframe 窗口的片段标识符。 子窗口通过监听hashchange事件得到通知。同样的，子窗口也可以改变父窗口的片段标识符。

  （2）跨文档通信API（Cross-document messaging）: 为window对象新增了一个window.postMessage方法，允许跨窗口通信，不论这两个窗口是否同源。
  ```

  `AJAX 请求:`

  ```text
  除了架设服务器代理（浏览器请求同源服务器，再由后者请求外部服务），有三种方法规避这个限制:

  （1）JSONP: 基本思想是，网页通过添加一个<script>元素，向服务器请求 JSON 数据，这种做法不受同源政策限制；服务器收到请求后，将数据放在一个指定名字的回调函数里传回来。

  （2）WebSocket: 使用ws://（非加密）和wss://（加密）作为协议前缀。该协议不实行同源政策。

  （3）CORS: 跨源资源分享（Cross-Origin Resource Sharing）
  ```
