#Javascript模块化编程


####**CommonJS/CMD(Common Module Definition)**

>- 同步加载————对于浏览器，等待加载时间长，容易造成假死状态(服务器端)。  
>- `CMD`采用了服务器优先的策略，采取同步行为，且`CMD`模块只支持对象作为模块。

```
   var math = require('math');
   math.add(2,3);
```
>返回一个模块对象  
>通过该模块对象执行具体操作
  

<br>
####**AMD (Asynchronous Module Definition)**###

>- 异步加载————模块加载不影响其他语句的执行。所以依赖该模块的语句，都定义在一个回调函数中，加载完成后，才执行回调函数。(客户端异步加载) 
>- `AMD`采用浏览器优先的方式来开发，选择了异步行为与简化的向后兼容性，但它完成没有文件`I/O`的概念。  
>- `AMD`支持对象、函数、构造器、字符串、JSON以及其他许多类型的模块，运行在浏览器本地环境之中。具有较好的灵活性。

```
require([module],callback);
```
>第一个参数[module]是一个数组，里面的成员是要加载的模块,第二个参数callback，则是加载成功之后的回调函数。

```
require(['math'],function(math){
   math.add(2,3);    
})
```  
>实现AMD规范的js库主要有`require.js`和`curl.js`    


<br>
####**UMD (Universal Module Definition)**
>- 通用模块定义——`UMD`定义那些既能够在客户端又能在服务器端工作的模块，这样的模块同时也能和目前可用的主流脚本加载器一同工作。  
>- `UMD`可以说是`CMD`及`AMD`的混合模式`require.js`符合`UMD`规范。  


<br>
####**AMD 与 CMD的区别 **
- 加载方式：`AMD`—— 异步加载；`CMD`—— 同步加载
- 使用环境：`AMD`—— 浏览器优先；`CMD`—— 服务器优先
- 模块定义：`AMD`—— 比较灵活；`CMD`—— 模块只能是对象
- 对于依赖模块：`AMD`—— 提前执行；`CMD`—— 延迟执行(as lazy as possible)
- 模块加载：`AMD`—— 依赖前置；`CMD`—— 依赖就近
 
```
// CMD
define(function(require, exports, module) {

    var a = require('./a')  
    a.doSomething()   
    // ....   
    
    var b = require('./b') 
    // 依赖可以就近书写   
    b.doSomething()   
    // ... 
})
```
```
// AMD 默认推荐的是
define(['./a', './b'], function(a, b) { // 依赖必须一开始就写好   

    a.doSomething()    
    // .....
    
    b.doSomething()    
    ...
})
```

####**阅读**

- [Learning JavaScript Design Patterns](http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/#modularjavascript)  
- [Javascript模块化编程](http://www.ruanyifeng.com/blog/2012/11/require_js.html)
- [使用 AMD、CommonJS 及 ES Harmony 编写模块化的 JavaScript](http://justineo.github.io/singles/writing-modular-js/)
- [Writing Modular JavaScript With AMD, CommonJS & ES Harmony](http://addyosmani.com/writing-modular-js/)
- [REQUIREJS API](http://www.requirejs.org/docs/api.html)
- [AMD (中文版)](https://github.com/amdjs/amdjs-api/wiki/AMD-(%E4%B8%AD%E6%96%87%E7%89%88))
- [CMD 模块定义规范](https://github.com/seajs/seajs/issues/242)
- [AMD 和 CMD 的区别有哪些？](http://www.zhihu.com/question/20351507/answer/14859415)