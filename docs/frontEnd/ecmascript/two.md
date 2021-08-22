# 函数

## 普通函数

参数的默认值，rest 参数。

```js
const f = ({ a, b } = {}, ...res) => {
  console.log(a + b); //2
  console.log(res); //  [1,2,3]
};
f({ a: 1, b: 1 }, 1, 2, 3);
```

<!-- ### rest

### 解构赋值和默认值 -->

## 箭头函数

es6 新增箭头函数。`=>`。简化函数写法。

使用注意：

- 箭头函数没有自己得 this，this 指向外层代码块得 this，同时没有 arguments。
- 不能使用 new 名命，无法作为构造函数使用。
- 不能使用 yield。

```js
const a = () => {
  console.log(this);
};
a(); //Window
```

## 闭包

什么是闭包：返回得函数使用了调用函数得变量，那么返回得函数就是闭包

```js
function demo() {
  const a = 0;
  return function A() {
    console.log(a);
  };
}
const b = demo();
b(); //0
```

A 函数会保存 demo 函数得变量，所以滥用闭包可能会造成内存泄漏。同时闭包会形成伪作用域。`console.dir(b)`打印如下：

<img src="./three_b.png" width="100%">

## 函数科里化

什么是科里化:把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术。

具体函数如下形式：

```js
const add = (a, b, c) => {
  console.log(a + b + c);
};
const _add = (a) => {
  //科里化后
  return (b) => {
    return (c) => {
      console.log(a + b + c);
    };
  };
};

add(1, 2, 3); //6
_add(1)(2)(3); //6
```

一个简易函数实现如下：

```js
const currying = (fun, _args) => {
  const length = fun.length;
  let args = _args || [];
  return (...res) => {
    args.push(...res);
    if (args.length < length) return currying.call(this, fun, args); //判断参数接收情况
    return fun.apply(this, args);
  };
};
add = (a, b, c) => {
  console.log(a + b + c);
};
const _add = currying(add);
_add(1, 5, 4); //10
_add(1)(5, 4); //10
_add(1)(5)(4); //10
```

<!--
## 递归 -->
