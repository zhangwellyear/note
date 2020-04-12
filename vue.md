### 什么是`Vue.js`
- `Vue.js`是目前最火的一个框架
- `React`是目前最流行的一个框架

### `MVC`与`MVVM`之间的对应关系
- `MVC`是后端的分层开发概念
- `MVVM`是前端视图层的概念，主要关注于视图层分离，`MVVM`把前端的视图层分成了三个部分：`Model`, `View`, `VM ViewModel`
`MVC`与`MVVM`图解
![MVC与MVVM图解](assets/vue/01.MVC和MVVM的关系图解.png)

### `vue`常用命令
- `v-cloak` —— 解决插值表达式闪烁的问题
- `v-text` —— 为某个标签中的数据，设置为 `data` 中的值
- `v-html` —— 将文本以 `html` 方式进行解析
- `v-bind` —— 为某个属性绑定 `data` 中的数据
- `v-on` —— 为某个元素的事件绑定函数
- `v-model` —— 双向绑定某个数据
- `v-if` —— 
- `v-show`

### `v-on`中的事件修饰符
+ `.stop` —— 阻止冒泡
+ `.prevent` —— 阻止默认事件
+ `.capture` —— 添加事件侦听器时使用事件捕获模式
+ `.self` —— 只当事件在该元素本身（比如不是子元素）触发时触发回调
+ `.once` —— 只执行一次

### 使用`class`样式
1. 数组或对象
+ 数组
```html
<h1 :class="['red', 'thin', {'active': isactive}]">这是一个邪恶的H1</h1>
```
+ 对象
```html
<h1 :class="{red:true, italic:true, active:true, thin:true}">这是一个邪恶的H1</h1>
```
2. 内联样式
+ 直接通过`:style`形式进行书写
```html
<h1 :style="{color: 'red', 'font-size': '40px'}">这是一个善良的H1</h1>
```
+ 在`data`中定义好样式对象，再将样式对象引入到元素中

### `v-if`和`v-show`
- `v-if`: 每次都会重新删除或创建元素
- `v-show`: 每次不会重新进行`DOM`的删除和创建操作，只是切换了元素`display: none`样式

### `v-for`和`key`属性
1. 迭代数组
2. 迭代对象中的属性
3. 迭代数字

当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用 “**就地复用**” 策略。如果数据项的顺序被改变，Vue将**不是移动 DOM 元素来匹配数据项的顺序**， 而是**简单复用此处每个元素**，并且确保它在特定索引下显示已被渲染过的每个元素。

为了给 Vue 一个提示，**以便它能跟踪每个节点的身份，从而重用和重新排序现有元素**，你需要为每项提供一个唯一 key 属性。

在使用`v-for`循环数据时，可以使用`in`一个过滤的`methods`方法，同时把过滤条件传递到方法参数中。

### 过滤器的实现
1. 私有过滤器
```js
filters: {
    dateFormat(input, pattern = "") {
      var dt = new Date(input);

      // 获取年月日
      var y = dt.getFullYear();
      var m = (dt.getMonth() + 1).toString().padStart(2, '0');
      var d = dt.getDate().toString().padStart(2, '0');

      // 如果 传递进来的字符串类型，转为小写之后，等于 yyyy-mm-dd，那么就返回 年-月-日
      // 否则，就返回  年-月-日 时：分：秒
      if (pattern.toLowerCase() === 'yyyy-mm-dd') {
        return `${y}-${m}-${d}`;
      } else {
        // 获取时分秒
        var hh = dt.getHours().toString().padStart(2, '0');
        var mm = dt.getMinutes().toString().padStart(2, '0');
        var ss = dt.getSeconds().toString().padStart(2, '0');

        return `${y}-${m}-${d} ${hh}:${mm}:${ss}`;
      }
    }
}
```
2. 全局过滤器
```js
Vue.filter('过滤器名称', (input, patter = "") => {...})
```

### 自定义键盘修饰符
```js
Vue.config.keyCodes.f2 = 113;
```

### 控制区域和对象
- `el` 指定要控制的区域
- `data` 对象
- `methods` 方法对象

### `Vue`的三大核心
+ 属性
  - 自定义属性
  - 原生属性
  - 特殊属性
+ 事件
  - 普通事件
  - 修饰符事件
+ 插槽
  - 普通插槽
  ```html
  <template slot="xxx"></template>
  <template v-slot:xxx></template>
  ```
  - 作用域插槽
  ```html
  <template slot="xxx" slot-scope="props"></template>
  <template v-slot:xxx="props"></template>  
  ```

### 过滤器的基本使用
定义：（注：过滤器处理函数也可以传递多个参数）
```javascript
Vue.filter('过滤器名称', (data, [arg1, arg2]) => {...})
```
使用：
```javascript
{{ name | '过滤器名称' }}
```

### 按键修饰符
以`enter`回车键为例
```javascript
@keyup.enter
@keyup.113 // F2键（通过键值的方式使用按键修饰符）
```
自定义全局按键修饰符
```javascript
Vue.config.keyCodes.f2 = 113;
```

### 自定义全局指令
```javascript
Vue.directive('focus', {
    // 在下面的每个函数中，第一个参数永远是 el，表示被绑定了指令的那个元素，el 参数是一个原生的 JS 对象
    bind: function (el, bindings) { // 每当指令绑定到这个元素上时，会执行该钩子函数
        el.style.color = bindings.value;
    },
    inserted: function (el) { // 表示元素插入到DOM中时，会执行 inserted 函数 【触发1次】
        el.focus;
    },
    updated: function () {  // 当 VNode 更新时，会执行 updated，可能触发多次

    }
})
```

### `Vue`实例的生命周期
+ 创建期间
  - `beforeCreated`: 实例刚在内存中创建，此时，还没有初始化好`data`和`methods`属性
  - `created`: 实例已经在内存中创建OK，此时`data`和`methods`已经创建OK，此时还未开始编译模板
  - `beforeMounted`: 此时已经完成了模板的编译，但是还未挂载到页面中
  - `mounted`: 此时，已经将编译好的模板，挂载到了页面指定的容器中
+ 运行期间
  - `beforeUpdate`: 状态更新之前执行此函数，此时`data`状态值是最新的，但是界面上显示的数据还是旧的，因为此时还没有开始重新渲染`DOM`元素
  - `updated`: 实例更新完毕后调用此函数，此时`data`中的状态值和界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了
+ 销毁期间
  - `beforeDestroy`: 实例销毁之前调用，在这一步，实例仍然完全可以使用
  - `destroyed`: `Vue`实例销毁后调用

### `Vue`的动画属性
+ `transition`
+ 四个类样式（两组）
  - `.v-enter`
  - `.v-leave-to`
  - `.v-enter-active`
  - `.v-leave-active`

### `Vue`的动画钩子函数
1. 定义`transition`组件和三个钩子函数
```html
<div id="app">
    <input type="button" value="切换动画" @click="isshow = !isshow">
    <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter">
      <div v-if="isshow" class="show">OK</div>
    </transition>
</div>
```
2. 定义三个`methods`钩子方法
```js
methods: {
    beforeEnter(el) { // 动画进入之前的回调
        el.style.transform = 'translateX(500px)';
    },
    enter(el, done) {
        el.offsetWidth;
        el.style.transform = 'translateX(0px)';
        done();
    },
    afterEnter(el) {
        this.isShow = !this.isShow;
    }
}
```
3. 定义动画过渡时长和样式：
```css
.show {
      transition: all 0.4s ease;
}
```

### `Vue.extend`定义全局组件
注意驼峰命名，使用时使用烤串命名
```javascript
var login = Vue.extend({
    template: '<h1>登录</h1>'
});
Vue.component('login', login);
```

### `vue.resource`配置根路径及表单形式上传
+ `Vue.http.options.root = 'http://localhost:3000;`
+ `Vue.http.options.emulateJSON = true;`

### `Vue`中的动画
```css
```

### 定义`Vue`组件
组件的出现，是为了拆分代码，减少代码量，能够以不同的组件，划分不同的功能模块
+ 模块化：从代码逻辑的角度进行划分，方便代码分层开发，保证每个模块的职能单一
+ 组件化：从UI界面的角度进行划分，便于UI重用

### `Vue`全局定义组件的三种方式
无论以什么方式创建出来的组件，都只有一个根元素
+ `extend` + `component`
```javascript
const com1 = Vue.extend({
    template: '<h3>这是 Vue.extend 创建出来的组件</h3>'
});

Vue.component('myCom', com1);
```
+ `component`直接创建
```javascript
Vue.component('mycom', {
    template: '<h3>这是 Vue.compoennt 创建出来的组件</h3>'
})
```
+ `template` + `component`
```html
<template id="tmp1">
    <h2>这是由 template 配合创建的组件</h2>
    <h3>超级好用，很不错！</h3>
</template>
```

### 私有组件的定义
`components`属性定义私有组件

### 组件中的`data`
1. 组件可以有自己的`data`数据;
2. 组件的`data`和实例的`data`有点不一样，实例中的`data`可以为一个对象，但是，组件中的`data`必须是一个方法;
3. 组件中的`data`除了必须为一个方法外，这个方法内部，还必须返回一个对象;
4. 组件中的`data`使用方式与实例中的`data`使用，完全一样。

### 父组件向子组件传值
```html
<com1 v-bind:msgParent="msg"></com1>
<!-- msg 为父组件中定义的属性值 -->
```
子组件中
```js
const vm1 = new Vue({
    data: {},
    methods: {},
    components: {
        com1: {
            template: '<h1>这是子组件 --- {{ msgParent }}',
            filters: {},
            directives: {},
            methods: {},
            props: ['msgParent']   // 唯一的数组
        }
    }
})
```
备注：`props`中的数据都是只读的，`data`中的数据是可读可写的

### 子组件向父组件传值
1. 在父组件中定义一个函数;
2. 组件标签中，绑定父组件的函数到某个事件（自定义名称）;
3. 在子组件中，通过`this.$emit('自定义名称', param1, param2)`的方式使用;
4. 父组件可以通过子组件`this.$emit`传入的参数，对父组件`data`进行修改

### 使用`ref`获取`DOM`元素
```html
<h3 id="myh3" ref="myh3"></h3>
```
使用`ref`作为属性的对象，在`vm`实例中，会将`<h3>`对象挂载到`$refs`对象中
组件也可以通过`ref`获取整个组件的引用，与`document.getElementById('myh3')`获取得到的内容相同，都是一个`DOM`元素。

### 路由的定义和使用
定义：
使用如下的方式进行定义
```js
new VueRouter({
    routes: [
        { path: '/login', component: login },
        { path: '/register', component: register }
    ]
})
```

### 选中路由的类的定义
`linkActiveClass`

### 路由规则中参数的定义
方式一：
1. 在规则中定义参数：
```js
{ path: '/register/:id', component: register }
```
2. 获取路由中的参数
```js
var register = Vue.extend({
    template: '<h1>注册组件 --- {{ this.$router.params.id }}</h1>'
})
```
方式二：
1. 在`router-link`中的`to`属性上定义
```html
<router-link :to="{path:'/one/log',query:{num:123}}"></router-link>
<router-link :to="{path:'/one/log',params:{num:123}}"></router-link>
```
2. 获取路由中的参数
```js
const register = Vue.extend({
    template: '<h1>注册组件 --- {{ this.$router.query.id }}'
})
```
方式三：
+ 使用模板字符串
```js
getDescribe(id) {
    // 直接调用$router.push 实现携带参数的跳转
    this.$router.push({
        path: `/describe/${id}`,
    })
}
```
+ 通过路由属性中的`name`来确定匹配的路由，通过`params`传递参数
```js
this.$router.push({
    name: 'Describe',
    params: {
    id: id
    }
})
```
+ 通过`path`来确定匹配的路由，通过`query`来传递参数
```js
this.$router.push({
    path: '/describe',
    query: {
    id: id
    }
})
```

### `query`与`params`的不同表现
1. 在`url`中采用`&`进行拼接的参数，可以通过`this.$route.query`获得;
2. 使用`/:id/:name`方式进行路由匹配传入的参数，可以通过`this.$route.params`获得。

### `computed`, `watch`和`methods`之间的对比
1. `computed`属性的结果会被缓存，除非依赖的响应式属性变化才会重新进行计算。主要当做属性来使用;
2. `methods`方法，表示一个具体的操作，主要书写业务逻辑;
3. `watch`一个对象，键是需要观察的表达式，值是对应的回调，主要用来监听某些特定数据的变化。

### `router-link`
使用`router`属性来使用路由规则
```js
const router = new VueRouter({
    routes: [
        { path: '/login', component: login },
        { path: '/register', component: register }
    ]
});

const vm = new Vue({
    el: '#app',
    router: router
})
```
可以使用`tag`属性指定`router-link`渲染的标签类型

### `babel`的配置
需要安装的包有：`babel-core`, `babel-loader`, `babel-plugin-transform-runtime`, `babel-preset-env`, `babel-preset-stage-0`
在`webpack.config.js`中设置项如下：
```javascript
{
    test: /\.js$/,
    use: 'babel-loader',
    exclude: /node_modules/
}
```
在`.babelrc`中设置项如下：
{
    "presets": ["env", "stage-0"],
    "plugins": []
}

以上是`webpack3`的使用，至于`webpack4`，还是看官网教程使用

### 解析`Vue`文件
需要安装`vue-template-compiler`, `vue-loader`包

### 常用的高级特性`provide`/`inject`
日常业务开发很少用到，底层通用组件多用

解决的问题：组件间通信问题

### template
+ 模板语法（HTML语言）
+ 数据绑定使用`Mustache`语法（双大括号）

抽象来看，组件可以区分为两类：一类是偏视图表现的，一类则是偏逻辑的

Vue中的`template`和`JSX`最终都会被编译成`createElement`

### vue中的`class`与`style`绑定
+ 对象语法（对象可定义于`Vue`实例中）
+ 数组语法（将每个属性列在中括号中，其值与`data`中绑定的值一致）
+ 组件上定义的（若组件的`template`模板中已有`class`相关的内容，使用时也存在`class`样式，那么在使用时的值，与`template`模板中绑定的值都将显示出来。

### 自定义按键修饰符别名
`Vue.config.keyCodes.f1 = 112`

### 一些表单输入需要注意的地方
+ 文本（多行文本） —— 直接双向绑定即可
+ 复选框 —— 单个复选框，使用一个`boolean`类型值即可，多个复选框，使用数组，选择后数组中存储的为复选框的`value`值
+ 单选按钮 —— 绑定的值会为选择的数据

### `vue`中的三个绑定事件修饰符
+ `.lazy` —— 数据在`change`时而非`input`时更新
+ `.number` —— 输入值只能为数值类型
+ `.trim` —— 去掉文本的首尾空白字符