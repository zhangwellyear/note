### `js`实现深拷贝
```javascript
function deep(obj, map = new WeakMap()) {
    if (typeof obj === 'object') {
        let newObj = Array.isArray(obj) ? [] : {};
        if (map.get(obj)) { // 循环引用
            return map.get(obj);
        }
        map.set(obj, newObj);
        for (const key in obj) {
            newObj[key] = deep(obj[key]);
        }
    } else {
        return obj;
    }
}
```

### `js`实现`call`/`apply`
```javascript
Function.prototype.call2 = function (context, ...args) {
    const func = this;
    const fn = Symbol('fn');
    context[fn] = func;
    let res = context[fn](...args);
    // let res = context[fn](args);    // apply的实现
    Reflect.deleteProperty(context, fn);
    return res;
}
```

### `js`实现`bind`
```javascript
Function.prototype.bind2 = function (context, ...args) {
    if (typeof this !== 'function') {
        throw new Error('error');
    }

    const func = this;
    const fn = Symbol('fn');
    context[fn] = func;
    
    const fBound = function () {
        const bindArgs = Array.prototype.slice.call(arguments);
        return context[fn].apply(this instanceof fBound ? this : window, args.concat(bindArgs));
    }

    fBound.prototype = Object.create(this.prototype);

    return fBound;
}
```

### `js`实现`debounce`防抖函数
```js
const debounce = (fn, delay) => {
    let timer = null;
    return (...args) => {
        clearTimeout(timer);
        timer = setTimeout(() =>{
            fn.apply(this, args);
        }, delay);
    }
}
```

### `js`实现`throttle`节流函数
```js
const throttle = (fn, delay = 1000) => {
    let flag = true;
    return (...args) => {
        if (!flag) return;
        flag = false;
        setTimeout(() => {
            flag = true;
            fn.apply(this, args);
        }, delay)
    }
}
```

### `js`实现`instanceof`
```js
function instanceof(left, right) {
    const proto = Object.getPrototypeOf(right);
    const left_proto = left.__proto__;

    while (true) {
        if (left_proto === null) return false;
        if (left_proto === proto) return true;

        left_proto = left_proto.__proto__;
    }
}
```

### `js`模拟实现`new`
```js
function myNew() {
    const obj = new Object();
    const Constructor = [].shift.call(arguments);
    obj.__proto__ = Constructor.prototype;

    const res = Constructor.apply(obj, arguments);

    return typeof res === 'object' ? res : obj;
}
```