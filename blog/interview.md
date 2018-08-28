<a name="20180828"></a>2018/08/28

### 跨域问题

跨域问题的出现是因为“同源策略”，出于安全考虑，javascript只能操作相同协议、端口以及域名中的资源或请求。

通过XHR实现Ajax通信:

```javascript
var request = new XMLHttpRequest();  // 源自 HTTP API
```





- JSONP，json with padding，参数式json。

  - 服务器端的响应采用JSON编码的数据格式，执行脚本时，js解析器能自动将其解码。

  ```javascript
  var script = document.createElement("script"); // script标签跟img元素，有能力不受限制地从其他域加载资源；
  script.src = "http://freegeoip.net/json/?callback=handleResponse";
  document.body.insertBefore(script,document.body.firstCgild);
  ```

  

- CORS，Cross-Origin Resource Share，跨源资源共享。

  - 用新的“Origin”请求头和新的“Access-Control-Allow-Origin”响应头来扩充http。
  - 定义了在访问跨域资源时，浏览器跟服务器该如何沟通。

- document.domain

  - 问题：同源问题会给使用多个子域的大站点带来问题。

  - 解决：把两个窗口包含的脚本的domain设置成相同的值，name这两个窗口就不再受同源策略的约束了。

    ```javascrip
    home.example.com
    orders.example.com
    
    document.domain = example.com；
    ```

- 跨文档消息

  - 通过window对象的postMessage发送数据，并在子页面中通过异步onMessage事件取出数据。

  ```javascript
  <iframe src="b.html">
  window.frames[0].postMessage(data,'/');
  
  // b.html的js中
  window.addEventListener("message",data=>{}）
  window.onMessage = function( messageEvent ){...}
  ```

  

### Flex

一行控制显示3个

第二行靠右显示

按顺序order

### Float

浮动特性、后边放块元素还是行内元素？？

清除浮动

是否脱离文档流

### 继承

实例继承

原型继承

### 原型链

描述

### 变量提升



### 会话存储 sessionStorage、LocalStorage

cookie

### 缓存问题

移动端清除缓存



### html5新特性

### rem

### 优化，你做了什么？







### 



