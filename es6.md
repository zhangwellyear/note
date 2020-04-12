### `let`和`const`命令
+ 不存在变量提升
+ 暂时性死区
+ 不允许重复声明变量
+ 块级作用域
+ `ES6`声明变量的6种方法
  - let
  - const
  - var
  - function
  - import 
  - class

### 变量的解构赋值
+ 从**数组**和**对象**中提取值 （要求等号两边的模式相同）
+ 允许指定默认值
+ **字符串**的结构赋值
+ **数值**和**布尔值**的结构赋值
+ 用途：
  - 交换变量的值
  - 从函数中返回多个值（**数组**或**对象**）
  - 函数参数定义 —— 很方便地将一组参数与变量名对应起来
  - 快速提取`JSON`对象
  - 为函数参数设置默认值
  - 遍历`Map`结构

### 字符串的扩展
+ `Unicode`表示法
+ `codePointAt()`, `String.fromCodePoint()`, `at()`, `normalize()` —— 都是针对`Unicode`表示提出的一些方法
+ `includes()`, `startsWith()`, `endsWith`, `repeat()`, `padStart()`, `padEnd()`
+ 模板字符串
+ `String.raw()` —— 用来充当模板字符串的处理函数

### 正则的扩展
+ 正则对象创建时，第二个对象可以用来指定修饰符（且会覆盖掉第一个修饰符）
+ 字符串对象的方法有：
  - `match()`
  - `replace()`
  - `search()`
  - `split()`
+ `u`修饰符，处理大的`unicode`字符
+ `y`修饰符，全局匹配，与`g`的不同：`y`修饰符会确保匹配必须从剩余的第一个位置开始
+ `RegExp`对象属性
  - `sticky`属性 （表示是否设置了`y`修饰符）
  - `flags`属性 （返回正则表达式的修饰符）

### 数值的扩展
+ 二进制（0b, 0B）、八进制的新写法（0o， 0O）
+ `Number.isFinite()`, `Number.isNaN()`
+ 全局对象的两个方法`parseInt()`, `parseFloat()`移植到了`Number`对象上面
+ `Number.isInteger`, `Number.EPSILON`, `Number.isSafeInterger()`
+ `Math.trunc()`, `Math.sign()`, `Math.cbrt`
+ 对数运算、指数运算
+ `Integer`数据类型 （提案）

### 函数的扩展
+ 允许函数的参数设置默认值（注意参数默认值的位置）
+ `length`属性值 （只返回非默认值的参数个数）
+ 作用域：默认值参数初始化会形成一个单独作用域
+ `rest`参数 （...变量名）
+ `name`属性：匿名函数不再返回空字符串
+ 箭头函数 （注意事项如下：）
  - 函数体内`this`对象即为定义时所在对象
  - 箭头函数不能当做构造函数（即不能使用`new`命令）
  - 不能使用`arguments`对象
  - 不可以使用`yield`命令，因此箭头函数用作`Generator`函数

### 数组的扩展
+ 扩展运算符 `...` —— 将一个数组转为逗号分隔的参数
+ 具有`Iterator`接口的对象都可以使用扩展运算符
+ `Array.from()`使用情况
  - 类数组遍历
  - 可遍历对象
+ `Array.keys()`, `Array.findIndex`, `Array.entries`, `Array.keys()`, `Array.values()`, `Array.includes()`
+ `Math.max(...[1, 2, 3])`, `arr.push(...arr2)`, `[1, 2, ...more]`

### 对象的扩展
+ 允许直接写入`变量`和`函数`
+ `Object.is()` —— 判断两个值是否相等 (1) +0, -0; (2) NaN
+ 允许将表达式放到方括号中，作为属性名存在
+ `Object.assign` —— `params`: 源对象, 目标对象
+ `for ... in` —— 循环遍历对象自身和继承的可枚举属性
+ `Object.setPrototypeOf()`/`Object.getPrototypeOf()`
+ `Object.keys()`, `Object.values()`, `Object.entries`

### Symbol
解决对象属性名冲突的问题
+ `Symbol`作为属性名，属性不会出现在`for ... in`, `for ... of`循环中
+ `Object.getOwnPropertySymbols`方法可以获取指定对象的所有`Symbol`属性
+ `Symbol.for()`, `Symbol.keyFor()`

### `Set`和`Map`数据结构
+ `Set` —— 类似于数组，但成员的值都是唯一的
+ `Set.prototype.constructor`: 构造函数，默认是`Set`函数
+ `Set.prototype.size`: 返回`Set`实例的成员总数
+ `Set`实例的方法分为两大类：`操作方法`和`遍历方法`
+ 操作方法:
  - `add(value)` —— 添加某个值，返回`Set`结构本身
  - `delete(value)` —— 删除某个值，返回一个布尔值，表示删除是否成功
  - `has(value)` —— 返回一个布尔值，表示参数是否为`Set`的成员
  - `clear()` —— 清除所有成员，没有返回值
+ 遍历方法:
  - `keys()` —— 返回键名
  - `values()` —— 返回值
  - `entries()` —— 返回键值对
  - `forEach()` —— 使用回调函数遍历每个成员
+ `WeakSet`与`Set`的异同:
  - `WeakSet`的成员只能是对象
  - `WeakSet`中的对象都是弱引用
+ `Map` —— 使得对象的键可以是一个对象
+ `Map`实例的属性和方法
  - `size`属性
  - `set(key, value)` —— 设置`key`所对应的键值，返回整个`Map`结构
  - `get(key)` —— `get`方法读取`key`所对应的键值，找不到`key`，返回`undefined`
  - `has(key)` —— `has`方法返回一个布尔值，表示某个键是否在`Map`数据结构中
  - `delete(key)` —— `delete`方法删除某个键，返回`true`，如果删除失败，则返回`false`
  - `clear()` —— `clear`方法清除掉所有成员，没有返回值
+ `Map`原生提供的遍历方法
  - `keys()`
  - `values()`
  - `entries()`
  - `forEach()`
+ `WeakMap`
  - `WeakMap`只接受对象作为键名（`null`除外）
  - `WeakMap`的键名所指向的对象不计入垃圾回收机制

### Proxy
`Proxy`可以理解为在目标对象前架设一个“拦截”层
+ `var proxy = new Proxy(target, handler)`
+ `Proxy`支持的所有拦截操作
  - `get(target, propKey, receiver)`
  - `set(target, propKey, value, receiver)`
  - `has(target, propKey, value, receiver)`
  - `deleteProperty(target, propKey)`
  - `ownKeys(target)`
  - `getOwnPropertyDescriptor(target, propKey)`
  - `defineProperty(target, propKey, propDesc)`
  - `preventExtensions(target)`
  - `getPrototypeOf(target)`
  - `getExtensible(target)`
  - `apply(target, object, args)`
  - `construct(target, args)`
+ `Proxy`实例的方法
  - `get()` —— 拦截某个属性的读取操作
  - `set()` —— 拦截某个属性的赋值操作
  - `apply()` —— 拦截函数的调用、`call`、`apply`操作
  - `has()` —— 拦截`HasProperty`操作
  - `construct` —— 用于拦截`new`命令
  - `deleteProperty()` —— 用于拦截`delete`操作
  - `defineProperty()` —— 拦截了`Object.defineProperty`操作
  - `getOwnPropertyDescriptor()`
  - `getPrototypeOf()`
  - `isExtensible()`
  - ...

### Reflect
作用：
1. 将`Object`对象的一些明显属于语言内部的方法，放到`Reflect`对象上
2. 修改某些`Object`方法的返回结果
+ `Reflect`一共有13个静态方法

### Promise对象
主要用于解决异步流程控制的问题
+ 当前循环得不到的结果，但未来的事件循环会给到你结果
+ 是一个状态机
  - `pending`
  - `fulfilled/resolved`
  - `rejected`

+ `.then`和`.catch`
  - `resolved`状态的`Promise`会回调后面的第一个`.then`
  - `rejected`状态的`Promise`会回调后面的第一个`.catch`
  - 任何一个`rejected`状态且后面没有`.catch`的`Promise`，都会造成 浏览器/Node环境的全局错误

+ 执行`then`和`catch`会返回一个新的`Promise`，该`Promise`最终状态根据`then`和`catch`的回调函数的执行结果决定
  - 如果回调函数最终是`throw`，该`Promise`是`rejected`状态
  - 如果回调函数最终是`return`，该`Promise`是`resolved`状态


异步编程的解决方案，主要用于解决回调地狱的问题
`Promise`对象的特点:
+ 对象的状态不受外界影响，`Promise`对象有三种状态：
  - `Pending` —— 进行中
  - `Fullfilled` —— 已成功
  - `Rejected` —— 已失败
+ 一旦状态改变，就不会再变
+ `Promise.prototype.then()`
+ `Promise.prototype.catch()`
+ `Promise.all()`
+ `Promise.race()`
+ `Promise.resolve()` —— 将现有对象转化为`Promise`对象
+ `Promise.reject()`
+ `done()` —— 保证抛出任何可能出现的错误
+ `finally()` —— 不管`Promise`对象最后状态如何都会执行的操作

指定`then`和`catch`会返回一个新的`promise`, 该`promise`最终状态根据`then`和`catch`的回调函数的执行结果确定

+ 如果回调函数最终是`throw`, 该`Promise`是`rejected`状态
+ 如果回调函数最终是`return`, 该`Promise`是`resolved`状态
+ 如果回调函数最终`return`了一个`Promise`, 该`Promise`会和回调函数`return`的`Promise`状态保持一致

### `async`/`await`
+ `async function`是`Promise`的语法糖封装
+ 异步编程的终极方案 - 以同步的方式写异步
  - `await`关键字可以"暂停"`async function`的执行
  - `await`关键字可以以同步的写法获取`Promise`的执行结果
  - `try-catch`可以获取`await`所得到的错误



### Iterator和for...of循环
