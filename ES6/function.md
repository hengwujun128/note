## 1.es6 函数参数和参数默认值

> 1.默认参数

> 2.默认参数对 arguments 对象的影响

> 3.默认参数表达式

> 4.默认参数临时性死区

> 5.rest 参数运算符(不定参数)

## 2.es6 构造函数

> 1.构造函数与扩展运算符

**rest 参数运算符出现在函数定义中，返回一个数组；扩展运算符出现在函数调用时，把数组转换成序列**

---

## 3.块级函数

**在代码块中申明一个块级函数严格来说是一个语法错误，但是所有的浏览器都支持这个特性，但是每个浏览器对这个特性支持稍有不同**

```
"use strict"
// es5
if(true){
  // error in es5
  function doSomething(){
  //
  }
}
//es6

if(true){
  console.log(typeof doSomething); // 'function'
  function doSomething(){
    //
  }
}
```

> 1.块级函数与 let 函数表达式的区别:块级函数会被提升到块的顶部，let 定义的函数表达式不会被提升;

```
"use strict"
if(true){
  console.log(typeof doSomething);   // 'error'
  let doSomething = function(){
    //
  }
  doSomething()
}
```

> 2.如果需要函数提升到代码块顶部，则选择块级函数；如果不需要，则选择 let 函数表达式

> 3.非严格模式下的块级函数

**在 es6 中，即使处于非严格模式下，也可以申明块级函数，但是其行为与严格模式稍有不同,这些函数不在提升到代码块顶部，而是提升到外围函数或全局作用域顶部**

```
//es6
if(true){
  console.log(typeof doSomething); //'function'
  function doSomething(){
    // 空函数
  }
  doSomething();
}
console.log(typeof doSomething) // 'function'
```

## 4.箭头函数

> 1.箭头函数与普通函数的区别(4)

* 没有 this,super,arguments,newTarget 绑定
* 不能通过 new 关键字调用(没有[[construct]]方法)
* 没有原型
* 不可以改变 this 绑定
