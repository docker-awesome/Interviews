# Interviews

`Common front-end interview questions.`

## JavaScript Basic

- ### Cookie, localStorage, sessionStorage 区别

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

- ### 同源政策（“同源”指的是”三个相同“：`协议相同`， `域名相同`， `端口相同`）

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

- ### script 脚本

  `工作原理:`

  ```text
  1. 浏览器一边下载 HTML 网页，一边开始解析。也就是说，不等到下载完，就开始解析。
  2. 解析过程中，浏览器发现<script>元素，就暂停解析，把网页渲染的控制权转交给 JavaScript 引擎。
  3. 如果<script>元素引用了外部脚本，就下载该脚本再执行，否则就直接执行代码。
  4. JavaScript 引擎执行完毕，控制权交还渲染引擎，恢复往下解析 HTML 网页。
  ```

  `defer 属性:`

  ```text
  1. 浏览器开始解析 HTML 网页。
  2. 解析过程中，发现带有defer属性的<script>元素。
  3. 浏览器继续往下解析 HTML 网页，同时并行下载<script>元素加载的外部脚本。
  4. 浏览器完成解析 HTML 网页，此时再回过头执行已经下载完成的脚本。
  ```

  `async 属性:`

  ```text
  1. 浏览器开始解析 HTML 网页。
  2. 解析过程中，发现带有async属性的script标签。
  3. 浏览器继续往下解析 HTML 网页，同时并行下载<script>标签中的外部脚本。
  4. 脚本下载完成，浏览器暂停解析 HTML 网页，开始执行下载的脚本。
  5. 脚本执行完毕，浏览器恢复解析 HTML 网页。
  ```

- ### 回流(reflow) 和 重绘(repaint)

  `浏览器渲染：`

  ```text
  1. 解析html生成DOM树，解析css，生成CSSOM树，将DOM树和CSSOM树结合，生成渲染树；
  2. 根据渲染树，浏览器可以计算出网页中有哪些节点，各节点的CSS以及从属关系 - 回流
  3. 根据渲染树以及回流得到的节点信息，计算出每个节点在屏幕中的位置 - 重绘
  4. 最后将得到的节点位置信息交给浏览器的图形处理程序，让浏览器中显示页面
  ```

  `回流：`

  ```text
  指的是当渲染树中的节点信息发生了大小、边距等问题，需要重新计算各节点和css具体的大小和位置。

  比如：
  盒模型的相关操作，定位相关操作，浮动相关操作会触发重新布局。
  改变节点的结构或其中的文本结构会触发重新布局。
  CSS: width, height, padding, border, margin, position, top, left, bottom, right, float, clear, text-align, vertical-align, line-height, font-weight, font-size, font-family, overflow, white-space
  ```

  `重绘：`

  ```text
  指当节点的部分属性发生变化，但不影响布局，只需要重新计算节点在屏幕中的绝对位置并渲染的过程

  比如：
  改变元素的背景颜色、字体颜色等操作会造成重绘。
  CSS: color, border-style, border-radius, text-decoration, box-shadow, outline, background
  ```

  `回流的过程在重绘的过程前面，所以回流一定会重绘，但重绘不一定会引起回流。`

- ### 防抖和节流

  `防抖：`

  ```text
  触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间。
  （每次触发事件时都取消之前的延时调用方法）
  ```

  `节流：`

  ```text
  高频事件触发，但在n秒内只会执行一次，所以节流会稀释函数的执行频率
  （每次触发事件时都判断当前是否有等待执行的延时函数）
  ```

- ### TCP 三次握手 和 四次挥手

  `三次握手：`

  ```text
  1. client -> server: 发送请求
  2. server -> client: 准备接受
  3. client -> server: 马上发送
  ```

  `四次挥手：`

  ```text
  1. client -> server: 请求保文发送完毕
  2. server -> client: 请求保文接收完毕
  3. server -> client: 响应保文发送完毕
  4. client -> server: 响应保文接收完毕
  ```

- ### XSS 和 CRSF

  `XSS: 跨站脚本攻击（Cross-Site Scripting）`

  `CRSF: 跨站请求伪造（Cross-site request forgery）`

- ### 事件机制 & 事件委托

  `DOM 事件流(Event Flow)存在三个阶段：事件捕获阶段、处于目标阶段、事件冒泡阶段。`

  ```text
  1. 事件捕获(Event Capturing)
  2. 事件冒泡(Dubbed Bubbling)
  ```

- ### 设计模式（Design Pattern）

  `六大设计原则(SOLID):`
  
  ```text
  总原则 - 开闭原则（Open Closed Principle）
  
  1. 单一职责原则 (Single Responsibility Principle)
  2. 里氏替换原则 (Liskov Substitution Principle)
  3. 依赖倒置原则 (Dependence Inversion Principle)
  4. 接口隔离原则 (Interface Segregation Principle)
  5. 迪米特法则 (Law of Demeter)
  6. 合成复用原则 (Composite Reuse Principle)
  ```

  `设计模式的三大类:`
  
  ```text
  1. 创建型模式 (Creational Pattern)
  2. 结构型模式 (Structural Pattern)
  3. 行为型模式 (Behavioral Pattern)
  ```
