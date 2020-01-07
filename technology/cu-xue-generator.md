---
description: 不求精细运用、先从思路上理解
---

# 【Generator学习1】粗学Generator

## Generator函数是什么？

它有多种理解角度。它具备暂停执行和继续执行的特点。它执行返回的hw是一个遍历器对象。

```text
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```

### Iterator接口（遍历器接口）是什么？

任何数据结构，只要具备遍历器接口，就可以去完成遍历操作。

具备遍历器接口的意思，即对象的Symbol.iterator属性是一个方法，这个方法执行能返回遍历器对象。

### 遍历器对象是什么。

hw即一个遍历器对象。遍历器对象能1次或者多次调用next方法，返回特定格式的数据。

```text
var it = makeIterator(['a', 'b']);

it.next() // { value: "a", done: false }
it.next() // { value: "b", done: false }
it.next() // { value: undefined, done: true }
```

### Generator函数能做什么？

* 执行能返回遍历器对象，可以给任何数据结构部署遍历器接口
* 用同步的方式写异步操作（通过暂停/启动，异步操作完成的时候启动）
* 可以作为协程的实现方式（多个任务同时在运行但同时只保持1个在执行，由协程来分配执行权）
* 控制多步操作（控制多个任务一个一个来执行）

{% embed url="https://es6.ruanyifeng.com/\#docs/generator" %}



