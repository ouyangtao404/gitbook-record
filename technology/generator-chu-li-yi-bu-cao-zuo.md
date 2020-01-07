---
description: Generator 函数将 JavaScript 异步编程带入了一个全新的阶段
---

# 【Generator学习2】Generator处理异步操作

## 利用Generator特性，用同步的编码方式来实现异步操作

我们知道Generator函数的执行，具备“暂停执行/继续执行”执行的特点。利用这个特点，在遇到异步操作时候用yield暂停，执行完成之后调用“启动”。

### Generator函数的数据交换和错处处理机制

```text
function* gen(x){
  var y = yield x + 2;
  return y;
}

var g = gen(1);
g.next() // { value: 3, done: false }
g.next(2) // { value: 2, done: true }
```

看上方代码，next方法可以接受参数，向Generator函数体内输入数据。

```text
function* gen(x){
  try {
    var y = yield x + 2;
  } catch (e){
    console.log(e);
  }
  return y;
}

var g = gen(1);
g.next();
g.throw('出错了');
// 出错了
```

看上方代码，指向对象抛出的错误，可以被Generator函数体内的try...catch捕获。

### 什么是Thunk函数

定义：多参数函数，替换成一个只接受回调函数作为参数的单参数函数。

```text
示例：

// 正常版本的readFile（多参数版本）
fs.readFile(fileName, callback);

// 使用Thunck函数（实现细节先忽略）
var readFileThunk = Thunk(fileName);
readFileThunk(callback);
```

任何函数，只要参数有回调函数，就能写成 Thunk 函数的形式。生产环境建议使用Thunkify模块。

### 运用Thunk函数来实现Generator函数（包含异步操作）自动执行

```text
var g = function* (){
  var f1 = yield readFileThunk('fileA');
  var f2 = yield readFileThunk('fileB');
  // ...
  var fn = yield readFileThunk('fileN');
};

run(g);
```

### co模块

用于支持Generator函数自动执行

```text
var gen = function* () {
  var f1 = yield readFile('/etc/fstab');
  var f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};

var co = require('co');
co(gen);
```

co模块支持并发的异步操作

```text
// 数组的写法
co(function* () {
  var res = yield [
    Promise.resolve(1),
    Promise.resolve(2)
  ];
  console.log(res);
}).catch(onerror);

// 对象的写法
co(function* () {
  var res = yield {
    1: Promise.resolve(1),
    2: Promise.resolve(2),
  };
  console.log(res);
}).catch(onerror);

// 另外一种写法
co(function* () {
  var values = [n1, n2, n3];
  yield values.map(somethingAsync);
});

function* somethingAsync(x) {
  // do something async
  return y
}
```

