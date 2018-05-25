## 1.what is cicular dependency?

"循环加载"（circular dependency）指的是，a 脚本的执行依赖 b 脚本，而 b 脚本的执行又依赖 a 脚本。

```
// a.js
var b=require('b')

// b.js
var a = require('a')
```

## 2.commonjs 模块加载原理

> 1.commonjs 一个模块就是一个文件，当 require 第一次加载脚本时候，就会执行整个脚本，在内存中生成一个对象

```
{
  id:'xx',      // ID属性是模块名
  exports:{},   // 就是模块输出的各个接口
  loaded:true   // 表示模块是否加载完毕
}
```

> 2.即使以后再 require 该模块也不会再次执行该模块,而是到缓存中取值

## 3.commonjs 模块的循环加载

> 1.  **commonjs 模块是加载时执行，一旦某个模块被循环加载,就只输出已经执行的部分,还未执行的部分不会输出**

[demo](http://www.ruanyifeng.com/blog/2015/11/circular-dependency.html)

## 4.es6 模块加载原理

> 1.每当 import 的时候，不会执行模块，只会生成一个引用，等到真正需要用的时候，在从模块中取值，即 es6 模块 是动态引用

```
// m1.js
export var foo = 'bar';
setTimeout(() => foo = 'baz', 500);

// m2.js
import {foo} from './m1.js';
console.log(foo);

setTimeout(() => console.log(foo), 500);


// output
```

m1.js 的变量 foo，在刚加载时等于 bar，过了 500 毫秒，又变为等于 baz。

> 2.**ES6 根本不会关心是否发生了"循环加载"，只是生成一个指向被加载模块的引用，需要开发者自己保证，真正取值的时候能够取到值。**
