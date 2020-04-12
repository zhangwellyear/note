### `nodejs`在业务中能做什么
可搭建运行于后台服务和浏览器前端之间的中间件

### `nodejs`可能会遇到的问题
+ 程序运行不稳定：经常出现服务器不可用的情况
+ 程序运行效率低：每秒能够处理的请求数维持在一个很低的水平
+ 培训困难，推广受阻：组里前端同学对服务端技术不熟悉

### `nodejs`开发应该掌握的技能
+ 开发调试
+ 框架设计
+ 性能优化
+ 灾备方案

### `nodejs`应用领域
+ `Web`服务
+ 开发工作流
+ 客户端应用

### 啥时候选择`nodejs`做服务端渲染
+ 搜索引擎优化 + 首屏速度优化 = 服务端渲染
+ 服务端渲染 + 前后端同构 = NodeJS

### `RPC`和`Ajax`的不同点
+ 不一定使用`DNS`作为寻址服务
+ 应用层协议一般不使用`HTTP`
+ 基于`TCP`或`UDP`协议

### `Ajax`和`RPC`通信的异同
+ 寻址和负载均衡：运维消化
+ 多路复用和二进制协议：`BFF`层实现

### `express`中配置`art-template`
#### 1. 安装
```shell
npm install --save art-template
npm install --save express-art-template
```
#### 2. 配置
```javascript
app.engine('art', require('express-art-template'));
app.set('views', path.join(__dirname, 'views'));
```

#### 3. 使用
```javascript
app.get('/', function (req, res) {
    res.render('index.art', {
        user: {
            name: 'aui',
            tags: ['art', 'template', 'nodejs']
        }
    });
});
```

### `express`配置解析表单`post`
安装：`body-parser`
配置：参考官方文档
获取：`req.body`

### 路由模块的抽取
`router`模块的定义
```javascript
const router = express.router();
router.get('/students', (req, res) => {});
router.post('/students', (req, res) => {});
module.exports = router;
```
`router`模块的引入
```javascript
const router = require('./router');
app.use(router);
```

### `body-parser`的挂载
应该在`app.use(router)`之前

### `koa`
+ 核心功能：
  - `express`在异步情况下不支持“洋葱模型”，但是`koa`可以通过`await`来完成
    + `ctx.status = 200`
    + `ctx.body = 'hello, world'`

### `RPC`调用
和`Ajax`相比的不同点
+ 不一定使用`DNS`作为寻址服务
+ 应用层协议一般不使用`HTTP`
+ 基于`TCP`或`UDP`协议

### 全双工通信与半双工通信

### 压力测试工具
+ `ab`
+ `webbench`