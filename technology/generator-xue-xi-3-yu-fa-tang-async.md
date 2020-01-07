---
description: async就是 Generator 函数的语法糖
---

# 【Generator学习3】语法糖async

### 

```text
const gen = function* () {
  const f1 = yield readFile('/etc/fstab');
  const f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};  
```

改成async函数：

```text
const asyncReadFile = async function () {
  const f1 = await readFile('/etc/fstab');
  const f2 = await readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

async特点：

* 内置执行器，asyncReadFile\(\) 执行即可
  * 不需要显式的处理yield吐出的内容去做g.next\(\)的衔接
* 语义更好
* 更广的适用性
  * 原来yield吐出的内容是有要求的，必须是promise或者thunk等可以做和g.next\(\)衔接的
  * async下，yield后面可以是promise或者其他原始类型的值。（原始类型的值如数值、字符串、布尔值。这些值都会被自动转成Promise对象）
* 返回值是Promise对象。且必须全部执行完才会执行回调

### async函数的多种形式

```bash
* 函数生命
    async function foo(){}

* 函数表达式
    const foo = async function(){};

* 箭头函数
const foo = async ()=>{}

* 对象的方法
    let obj = {
        async foo(){};
    }

* Class的方法
class Storage(){
    async doSth(){}
}
```

### 注意点

* 我若中间有异步操作失败，会中断后续执行。若想这种情况也继续执行，需要对错误有处理（用try...catch来兜住，或promose的情况用catch兜住）
* 若多个异步操作相互没有依赖，可以将多个promise合并成1个。

```text
let [foo, bar] = await Promise.all([getFoo(), getBar()]);
```

* 了解async的实现原理，就是将 Generator 函数和自动执行器，包装在一个函数里
* 了解并发获取资源并依次输出结果的实现方式
* 了解“顶层 await ”的预发提案

### 写个例子

```text
function readFile(fileName, success = true) {
  return new Promise((resolved, reject) => {
    setTimeout(() => {
      let text = `【我是文件${fileName}的文本内容】`;
      if (success) {
        resolved(text);
      }
      reject(new Error(`错误示例:${fileName}读取失败`));
    }, 50);
  });
}

async function ReadAllFile() {
  let f1 = await readFile("file1");
  let f2 = await readFile("file2");
  let f3 = await readFile("file3", false);
  let f4 = await readFile("file4");
  return {
    f1,
    f2,
    f3,
    f4
  };
}
let p = ReadAllFile();
p.then(dt => {
  console.log("dt", dt);
}).catch(err => {
  console.log("catch", err);
});

```



