# 测试框架jasmine
- `jasmine`是一个测试框架
- `karma`是一个任务运行器

## `jasmine`支持三种管理异步工作的方式
- `async/await` —— 隐式返回一个`promise`
- `Promise`
- 回调
若`Jasmine`没有检测到其中之一，将假定工作是同步的。同步的函数一旦返回`jasmine`会马上移动到下一个队列中。
同步的机制可以应用于`beforeEach`, `afterEach`, `beforeAll`, `afterAll`和`it`

### `async`/`await`
如果在`beforeAll`或者`afterAll`中存在`rejected`的`promises`，会造成单元测试/套件的失败。
如果一个`it`单元测试用例中以`async`修饰函数，在这个函数中使用`await`等待`Promise`
```ts
beforeEach(async function() {
  await someLongSetupFunction();
});

it('does a thing', async function() {
  const result = await someAsyncFunction();
  expect(result).toEqual(someExpectedValue);
});
```

### `done`
异步中使用的`done`函数只会调用一次，调用完成后

- `done`函数也可以直接强制使一个测试用例失败，`done.fail()`
  ```ts
  beforeEach(function(done) {
    setTimeout(function() {
        try {
        riskyThing();
        done();
        } catch (e) {
        done.fail(e);
        }
    });
  });
  ```

jasmine3.0之后，就可以直接传给`done`函数一个`error`，来直接使测试用例失败
```ts
beforeEach(function(done) {
  setTimeout(function() {
    var err = null;

    try {
      riskyThing();
    } catch (e) {
      err = e;
    }

    done(err);
  });
});
```

`router-outlet`未定义问题，往往是由于在`module`中未导入`RouterTestingModule`引起的