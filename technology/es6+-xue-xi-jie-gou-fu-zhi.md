---
description: 数组和对象的解构赋值
---

# \[ES6+学习\]解构赋值

### 数组的解构赋值

```text
let [a, b, c] = [1, 2, 3];
```

* 模式匹配
  * 左右保持同样的模式，左侧模式中的变量就会被赋为相应的值，若匹配不上则赋值为undefined
* 不完全解构
  * 左边模式只匹配一部分右边的数组，也可以解构成功。如let \[x, y\] = \[1, 2, 3\];
* 不是数组会报错。（严格说是不具备遍历器接口的数据）
  * 是否可解构取决于右侧结构是否具备Iterator接口，不具备则会报错。
* 指定默认值：let \[foo = true\] = \[\];
  * 若变量匹配到的值**严格等于undefined**，会被赋予默认值（包括let \[x = 1\] =\[undefined\]）
  * 惰性求值

### 对象的结构赋值

```text
//常规简写：
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
//等价完整写法：
let { foo:foo, bar:bar } = { foo: 'aaa', bar: 'bbb' };
```

* 靠属性名称匹配。
  * 若匹配不上则取不到值：let {foo} = {bar: 'baz'};
* 变量名和属性名不一致的情况
  * 使用完整写法结构：let { foo:x, bar:y } = { foo: 'aaa', bar: 'bbb' }; 
* 嵌套赋值：let { p: \[x, { y }\] } = obj;
  * （记住一点原则：key:value  赋值的永远是冒号的右侧变量value，若value不是变量，就继续拆开，右侧赋值的原则不变。）
  * 按照完整的解构写法去观察，就能分清模式和变量。
  * 更灵活复杂的嵌套赋值：
    * let obj = {};

      let arr = \[\];

      \({ foo: obj.prop, bar: arr\[0\] } = { foo: 123, bar: true }\);
  * 嵌套乱套的情况会报错
    * let {foo: {bar}} = {baz: 'baz'};  foo下是undefined，相当于{bar}=undefined会报错
* 可以取到继承的属性\(原型链上的可以取到\)
* 赋默认值，和数组特性基本一致（注意：null不算undefined，是===严格相等判断）
* 已经申明的变量要注意格式问题
  * let x;

    \({x} = {x: 1}\);
* 左侧允许没有变量，合法但没意义\({} = \[true, false\]\);
* 数组本质是特殊对象，可以进行对象属性解构  
  * let arr = \[1, 2, 3\];

    let {0 : first, \[arr.length - 1\] : last} = arr;

### 字符串的解构赋值

* 字符串是类似于数组的对象，可以等同数组来处理
* length属性，类似数组对象都有，可以进行属性解构赋值：let {length : len} = 'hello';

### 数值和布尔值的解构赋值

* 解构赋值规则：只要等号右边不是对象和数组，就先转为对象。所以，对于无法转为对象的undefined和null，解构会报错。
* 数值和布尔值的包装对象都有toString属性

```text
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```

### 函数参数的解构赋值

```text
function add([x, y]){
  return x + y;
}
```

* 【为函数参数指定默认值】和【为变量指定默认值】的区别：

```text
//给变量想x、y指定默认值
function move({x = 0, y = 0} = {}) {
  return [x, y];
}
move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]

//给函数指定默认值
function move({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}
move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, undefined]
move({}); // [undefined, undefined]
move(); // [0, 0]
```

理解方式:  function foo\(left = right\) {}

right是函数的参数默认值，left是解构的左侧。**一旦实际调用传了值，则right没有作用**。

### 应用场景

* 交换值
  * \[x, y\] = \[y, x\];
* 取值
  *  let \[a, b, c\] = obj;
* 函数参数的定义（也是取值，其实就是函数参数部分的取值）
  * function f\(\[x, y, z\]\) { ... }
* 提取json数据
  * let { id, status, data: number } = jsonData;
* 函数参数的默认值  \(避免写判断\)
  * function \(url, {

      async = true,

      beforeSend = function \(\) {}

    } = {}\) {

      // ... 

    };
* 遍历Map结构
* 输入模块的指定方法

### 注意事项

* 圆括号的使用
  * 不能使用的情况（只要有可能导致解构的歧义，就不得使用圆括号）
    * 变量声明
    * 函数参数（其实也是声明函数内部的变量）
    * 模式部分（有点难区分）
  * 可以使用的情况只有一种：非模式部



