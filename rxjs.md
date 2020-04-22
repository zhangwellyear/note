### 特点
+ 强大的功能性方法处理事件
+ 从命令式到声明式的思维转换

### 可观察对象
+ 可观察对象支持在发布者和订阅者之间传递消息

### 优势：
+ 事件处理
+ 异步编程
+ 处理多个值

### 常用操作符
+ `empty`会立即完成
+ `of`会从一个序列（数组，Map，字符串）创建一个`Observable`值

### 错误处理
+ 要在`catch`函数中返回一个`Observable`

### 多播处理
+ 使用`Subject`对象构建
  ```ts
  example.pipe(multicast(() => new Subject()))
  ```
+ 订阅过程中重放值的能力是区分`share`和`shareReplay`的关键

### 组合
+ `combineLatest`直到每个`observable`都至少发出一个值后才会发出初始值
+ `concat`前一个`observable`完成了再订阅下一个`observable`发出的值
+ `concat`从`rxjs/operators`中导入，作为实例方法
+ `concat`从`rxjs`中导入，作为静态方法
+ 当有一组`observables`, 只关心每个`observable`最后发出的值，该操作符最为合适
+ `pairwise`返回一对数字，一个是当前值，一个是前一个值
+ `startWith`改变起始值
+ `withLatestFrom`获取传入的`Observable`的最新值