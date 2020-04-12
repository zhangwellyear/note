### `Doctype`的作用
告知浏览器使用什么文档解析该文档
设置不正确会出现混杂模式（兼容模式）

+ 标准模式：排版和`JS`的运行，都是以浏览器支持的最高标准运行
+ 兼容模式：页面向后兼容，即模拟老式浏览器的行为防止站点无法运行

### `inline-block`及`img`存在对不齐的现象
主要基线问题，英文字母会有上行字母和下行字母的对齐问题

### 语义化标签
+ `<header>`
+ `<aside>`
+ `<nav>`
+ `<section>`
+ `<footer>`

### 新标签
+ `<canvas>`
+ `<vedio>`
+ `<audio>`

### 新的表单控件
+ `calendar`
+ `date`
+ `time`
+ `email`
+ `url`
+ `search`

### 新的技术
+ `webworker`
+ `websocket`
+ `geolocation`

### 常见的块级元素和行内元素
行内元素：
+ `a`
+ `b`
+ `span`
+ `img`
+ `input`
+ `select`
块级元素
+ `ul`
+ `ol`
+ `div`
+ `li`
+ `p`

### `link`和`@import`的区别
`link`属于`XHTML`标签，除了加载`css`外，还能定义`RSS`，定义`rel`连接属性等作用
`@import`是`css`提供的，在`css2.1`之后提供，只能加载`css`，且存在兼容性问题

### 常见的浏览器内核
+ `Trident` —— `IE`, `搜狗`, `360`
+ `Gecho` —— `NetScape6`及以上版本
+ `Presto` —— `Opera7`及以上 [`Opera`现内核也为`Blink`]
+ `Webkit` —— `Safari`, `Chrome` [`Chrome`现内核为`Blink`]

### `cookies`, `sessionStorage`和`localStorage`的区别
+ 传输的区别：
  - `cookie`数据始终在同源的`http`请求中携带，在浏览器和服务器之间来回传递
  - `sessionStorage`和`localStorage`不会存在传递，仅保存在本地
+ 传输大小的限制：
  - `cookie`一般不能超过4k
  - `sessionStorage`和`localStorage`存储更大，一般可以达到5M
+ 有效时间：
  - `localStorage` 存储持久数据
  - `sessionStorage` 数据在浏览器窗口关闭后自动删除
  - `cookie` 根据过期时间来判断

### `iframe`的优缺点
+ 缺点：
  - 会阻塞主页面的`onload`事件
  - 不利于`SEO`
  - `iframe`和主页共享连接池，浏览器对相同域的连接有限制，会影响页面的并行加载

### `label`标签的作用
用来关联某个标签，方便用户操作，点击`label`的范围即可触发绑定的标签事件

