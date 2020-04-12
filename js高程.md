`偏移量属性都是只读的，每次访问它们都需要重新计算`
`客户区大小也是只读的，每次访问也需要进行重新计算`

`scrollHeight` —— `元素内容的总高度`
`scrollWidth` —— `元素内容的总宽度`
`scrollLeft` —— `被隐藏在内容区域左侧的像素数`
`scrollTop` —— `被隐藏在内容区域上方的像素数`
`clientX`&`clientY` —— `表示事件发生时鼠标指针在视口中的水平和垂直距离`
`pageX`&`pageY` —— `表示鼠标光标在页面中的位置`
`screenX`&`screenY` —— 可以确定鼠标事件发生时，鼠标指针相对于整个屏幕的坐标信息

`shiftKey`, `ctrlKey`, `altKey`和`metaKey`这些属性中包含的都是布尔值，相应的键被按下，值为`true`

#### 客户区大小
指的是元素内容及其内边距所占据的空间大小。

遍历树的常用方法：
+ `createNodeIterator`
+ `createTreeWalker`

范围：
`createRange()`
新创建的范围直接与创建它的文档关联在一起，不能用于其他文档

`事件流描述的是从页面中接收事件的顺序`

"DOM2级事件"规定的事件流包括三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段
"DOM2级事件"定义了两个方法，用于处理指定和删除事件处理程序的操作：`addEventListener`和`removeEventListener`

将事件处理程序添加到事件流的冒泡阶段，这样可以最大限度地兼容各种浏览器

事件对象`event`包含所有与事件有关的信息，包括导致事件的元素，事件的类型以及其他与特定事件相关的信息
事件绑定的函数内部，`this`值始终等于`currentTarget`的值

事件对象的`eventPhase`属性，可用来确定事件当前正位于事件流的哪个阶段
捕获阶段：`eventPhase == 1`
位于目标对象上：`eventPhase == 2`
冒泡阶段：`eventPhase == 3`

图像元素不一定要从添加到文档后才开始下载，只要设置了src属性就会开始下载

焦点事件：
`document.hasFocus()`方法及`document.activeElement`属性配合

`DOMContentLoaded`事件则在形成完整的`DOM`树之后就会触发
`pageshow`事件在页面显示时触发
`hashchange`事件在URL的参数列表(及URL中“#”后面的所有字符串)发生变化时通知开发人员

“事件处理程序过多”问题的解决方案就是事件委托，事件委托利用了事件冒泡，只指定一个事件处理程序处理相应的事件。
使用事件委托，只需在DOM树中尽量最高的层次上添加一个事件处理程序

每个表单字段都有两个方法：`focus()`和`blur()`

`HTML5`为文本字段新增了`pattern`属性

选择框的`type`属性不是`select-one`，就是`select-multiple`

选择框的`change`事件只要选中了选项就会触发，其他表单字段的`change`事件是在值被修改且焦点离开当前字段时触发

`context.save()`方法保存的知识对上下文的设置和变换，不会保存绘图上下文的内容
`context.toDataURL()`方法可以获得绘制在`canvas`上的内容
`context.createRectLinearGradient()` —— 创建矩形渐变
`context.createRadialGradient()` —— 创建径向渐变

#### WebGL
`WebGL`涉及的复杂计算需要提前知道数值的精度，标准`JavaScript`数值无法满足需要，`WebGL`引入了一个概念，叫类型化数组。

每个`ArrayBuffer`对象表示的只是内存中指定的字节数

调用`gl.bindBuffer()`可以将`buffer`设置为上下文的当前缓冲区，调用该函数后，后续所有缓冲区操作都直接在`buffer`中执行。

`WebGL`操作一般不会抛出错误，手工调用`gl.getError()`方法

##### gl使用着色器的步骤
1. 创建顶点着色器
+ `gl.createShader(gl.VERTEX_SHADER)`
+ `gl.shaderSource(vertexShader, vertexGlsl)`
+ `gl.compileShader(vertexShader)`
2. 创建片元着色器
+ `gl.createShader(gl.FRAGMENT_SHADER)`
+ `gl.shaderSource(fragmentShader, fragmentGlsl)`
+ `gl.compileShader(fragmentShader)`

#### drag拖动事件
拖动某个元素时:
`dragstart`
`drag`
`dragend`

拖动到一个有效的放置目标上时
`dragenter`
`dragover`
`dragleave`/`drop`


嵌入多个`<source>`标签来解决浏览器不能支持所有媒体格式的问题

通过`canPlayType()`检测浏览器所能够播放的视频格式、音频格式

跨文档消息传递API能够让我们在不降低同源策略安全性的前提下，在来自不同域的文档间传递消息
历史状态管理让开发人员不必卸载当前页面即可修改浏览器的历史状态栈

错误处理后台开发人员通常要考虑类型、频率，或者其他重要的标准对错误进行分类。

### 错误处理
#### `finally`
无论是`try`还是`catch`还是`return`，都无法阻止`finally`子句的执行
```js
function testFinally() {
    try {
        return 2;
    } catch {
        return 1;
    } finally {
        return 0;
    }
}
```
上面的结果，无论如何都会返回0，`try`中的`return`语句被忽略

#### `ECMA-262`定义了7种错误类型
+ `Error` —— 基类型，其他错误类型都继承自该类型，主要供开发人员抛出自定义错误
+ `EvalError` —— 使用`Eval`函数发生异常时被抛出
+ `RangeError` —— 数值超出相应范围时触发，例如`new Array(-20)`
+ `ReferenceError`
+ `SyntaxError`
+ `TypeError` —— 执行特定于类型的操作时，变量的类型不符合要求所致
+ `URIError`

`throw`操作符指定的值没有类型要求

一般来说，需要关注三种错误：
+ 类型转换错误
+ 数据类型错误
+ 通信错误