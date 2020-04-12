### 常见布局
#### 水平居中
```html
<div class="parent">
    <div class="child"></div>
</div>
```
+ `margin`
```css
.parent {
    background-color: gray;
    height: 300px;
}

.child {
    width: 500px;
    height: 200px;
    background-color: #333;
    margin: 0 auto;
}
```

+ `inline-block` + `text-align`
```css
.parent {
    background-color: gray;
    height: 300px;
    text-align: center;
}
.child {
    width: 500px;
    height: 200px;
    background-color: #333;
    display: inline-block
}
```

+ `absolute` + `transform`
```css
.parent {
    background-color: gray;
    height: 300px;
    position: relative;
}
.child {
    width: 500px;
    height: 200px;
    background-color: #333;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
}
```

+ `flex`
```css
.parent {
    background-color: gray;
    height: 300px;
    display: flex;
    justify-content: center
}
.child {
    width: 500px;
    height: 200px;
    background-color: #333;
}
```
#### 垂直居中
+ `inline-block` + `vertical-align`
```css
.parent {
    background-color: gray;
    height: 300px;
    display: table-cell;
    vertical-align: middle;
}
.child {
    width: 500px;
    height: 200px;
    background-color: #333;
}
```

+ `absolute` + `transform`
```css
.parent {
    background-color: gray;
    height: 300px;
    position: relative;
}
.child {
    width: 500px;
    height: 200px;
    background-color: #333;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
}
```

+ `flex` + `align-items`
```css
.parent {
    background-color: gray;
    height: 300px;
    display: flex;
    align-items: center;
}
.child {
    width: 500px;
    height: 200px;
    background-color: #333;
}
```

#### 水平垂直居中
+ `inline-block` + `table-cell` + `text-align` + `vertical-align`
```css
.parent {
    background-color: gray;
    height: 300px;
    width: 800px;
    display: table-cell;
    vertical-align: middle;
    text-align: center;
}
.child {
    width: 500px;
    height: 200px;
    background-color: #333;

    display: inline-block;
}
```

+ `absolute` + `transform`
```css
.parent {
    background-color: gray;
    height: 300px;
    /* width: 800px; */
    position: relative;
}
.child {
    width: 500px;
    height: 200px;
    background-color: #333;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
```

+ `flex`
```css
.parent {
    height: 200px;
    background-color: gray;
    display: flex;
    align-items: center;
    justify-content: center;
}
.child {
    width: 200px;
    height: 80px;
    background-color: #333;
}
```

### `animation`与`transition`
+ `transition`: 过渡，指一个属性的变化是逐渐完成的
下面的例子是当鼠标放到`box`元素上时，放大两倍，这个过程不是一下子完成的，设置`transition`属性后，存在一个过渡
```css
.box {
    width: 100px;
    height: 100px;
    transition: transform 1s ease-in infinite;
}
.box:hover {
    transform: scale(2, 2);
}
```
+ `animation`: 动画，作为动画需要设置关键帧
```css
@keyframes myanimation {
    10%: {
        
    }
}
```

### `position: sticky`的实现
粘性定位`sticky`相当于相对定位`relative`和固定定位`fixed`的结合；页面元素滚动过程中，若某个元素距离其父元素的距离达到`sticky`粘性定位要求时，元素的`relative`效果变为固定定位`fixed`

使用场景：当需要给某个元素吸顶时，直接使用`sticky`属性即可

#### `sticky`属性使用条件
+ 父元素不能使用`overflow: hidden`或者`overflow: auto`
+ 必须指定`top, bottom, left, right`4个值之一，否则只会处于相对定位状态
+ 父元素的高度不能低于`sticky`元素的高度
+ `sticky`元素只在其父元素内生效

### `em`和`rem`的相同点和区别
#### 相同点：
+ 都不受`font-size`的变化影响

#### 不同点
`em` —— 相对长度单位，相对于当前对象内文本的字体尺寸
`rem` —— 也是相对长度单位，不过相对的是`HTML`根元素

### `opacity`与`rgba`之间的区别
+ `opacity`属性不仅让背景具有透明度，还使前端色具有相同的透明度，且其后代元素都将继承其透明度
+ `RGBA`只是对应属性设置了`RGBA`才会有效，不会影响到元素其他属性或者其他元素的样式风格
+ `opacity`只能为元素的背景设置透明度（会影响元素前景色），`RGBA`可以对元素任何具有颜色的属性设置

### 外轮廓与`border`的区别
+ 外轮廓不占用网页布局空间，不一定是矩形
+ 外轮廓是属于一种动态样式，只有元素获取到焦点或者被激活时呈现

### 多列布局`Column`相关
+ `column-width`属性类似于给列定义一个最小宽度(min-width)
+ `column-rule`理解上类似于`border`属性，但`column-rule`不占用任何空间位置。

### `transform-style`主要有两个属性值
+ `flat`
+ `preserve-3d`

### CSS 2D变形
镜像只能通过`matrix`矩阵实现

### 媒体查询
1. `max-width`
指媒体类型小于或等于指定的宽度时，样式生效

2. `min-width`
指媒体类型大于或等于指定的宽度时，样式生效

3. `max-device-width`
根据设备屏幕的输出宽度来进行媒体查询

4. `not`关键词
用来排除某种制定的媒体类型