以下为本书 2016 年 10 月第 1 版的勘误列表，欢迎提交 PR 进行补充，帮助其他读者。

### [1.1.1 语言特性] const、let 关键字

第一段示例代码：单引号错误，另 `console.log` 的参数应该是 `a`。勘正后为：

```javascript
if (true) {
  let a = 'name';
}
console.log(a);
// ReferenceError: a is not defined
```


### [1.1.1 语言特性] 函数 this在箭头函数中

第一段代码示例：结果错误 这里的 this.age 在setTimeout中应该是 undefined。

```javascript
let age = 2;
let kitty = {
  age: 1,
  grow: function() {
    setTimeout(function() {
      console.log(++this.age);
    }, 100);
  }
};

kitty.grow();
// 3

```
应修改为 var age ＝2;
因为：
`At the top level of programs and functions, let, unlike var, does not create a property on the global object.`
但是这段代码在 babel 编译后可以正常运行，所以笔者出现了这个错误。原因是 Babel 编译后并没有对这个特性没有特殊的处理。

附代码 Babel 编译后的结果：

```javascript
"use strict";

var age = 2;
var kitty = {
  age: 1,
  grow: function grow() {
    setTimeout(function () {
      console.log(++this.age);
    }, 100);
  }
};

kitty.grow();
```
### [3.4.1 props属性] 代码段export default Class 中的Class应为 class关键字
