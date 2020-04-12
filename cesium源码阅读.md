### `Cesium3DTileBatchTable.js`
参数详解：
`content`: 表示数据内容
`featuresLength`: 特征数据的长度
`batchTableJson`: 批量表的Json格式
`batchTableBinary`: 批量表的二进制格式
`colorChangedCallback`: 改变数据样式的回调函数

### `Appearance.js`
对外观渲染的`GLSL`和渲染状态进行记录

### `AttributeType.js`
对`WebGL`中的一些数据类型常量如`VEC2`, `VEC3`等相关字符串定义为对象，方便后续处理

### `Axis.js`
将一些坐标轴X, Y, Z对应的数字码以及坐标轴方向转换的矩阵，存储于`Axis`对象中

### `Batched3DModel3DTileContent.js`
从`tileset`中拿到出`tile`，并对`tile`根据`batchTable`数据存储的特点（3D Tiles规范）进行解析

#### `update`
`Batched3DModel3DTileContent`实例对象所拥有的`update`函数，是该文件中除初始化外比较重要的一个函数，该函数中，当解析后的`content`（`Batched3DModel3DTileContent`对象，在初始化时，`this`即为`content`），内容状态为`READY STATE`时，才会生成相应的绘制命令

### `BatchTable.js`
主要用于解析批量表中的属性数据

### `BillBoard.js`
将一些图标，图片之类的内容加载到三维场景中

### `BillBoardCollection.js`
用于管理`BillBoard`数据，可以猜到常用的函数有`add`, `remove`, `removeAll`

### `BlendEquation.js`
将`WebGL`中的几种与`blending`相关的常量封装到`BlendEquation`对象中

### `BlendFunction.js`
将`WebGL`中的几种`blend factor`相关常量封装到`BlendFunction`对象中

### `BlendingState.js`
这个不用说了，自然就是将`blending`相关的状态封装成对象

### `BlendOption.js`
这个是将`Blending`的几种模式封装到`BlendOption`对象中
+ `Opaque` —— 0
+ `Translucent` —— 1
+ `Opaque_And_Translucent` —— 2

### `BoxEmitter.js`
将粒子从某个盒子的中心发射，粒子速度自己有

### `BrdfLutGenerator.js`
主要用`BrdfLutGenerator`对象存储帧缓冲区，颜色纹理，绘制命令等

#### `createCommand`
这是创建绘制命令的一个函数，在使用过程中，将`framebuffer`和`renderstate`一起进行封装，调用`context.createViewportQuadCommand`创建绘制命令

#### `createFrameBuffer`
通过`new Texture({options})`对象的方式来创建纹理信息

### `Camera.js`
记录相机的一些信息

### `CameraEventAggregator.js`
记录相机的一些操作信息，如：鼠标左键，鼠标右键，滚轮，surface的双指操作（`PINCH`）

### `CameraEventType`
使用一个对象，将鼠标的不同操作对应到数字

