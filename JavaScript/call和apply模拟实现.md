## **JavaScript系列之模拟实现call和apply**

#### 概念：call和apply => 用于改变函数运行时上下文
call() 方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。
apply() 方法调用一个具有给定this值的函数，以及作为一个数组（或类似数组对象）提供的参数。

#### 实现：
```js
Function.prototype.newCall = function (context) {
  context = context || window;
  context.fn = this;

  const args = Array.from(arguments).slice(1);
  const result = context.fn(...args);

  delete context.fn;
  return result;
};

Function.prototype.newApply = function (context) {
  context = context || window;
  context.fn = this;

  let result;
  // 判断是否需要存储第二个参数
  if (arguments[1]) {
    result = context.fn(...arguments[1]);
  } else {
    result = context.fn();
  }

  delete context.fn;
  return result;
}
```
