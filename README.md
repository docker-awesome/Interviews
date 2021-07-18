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

- 同源政策（“同源”指的是”三个相同“：协议相同， 域名相同， 端口相同）
