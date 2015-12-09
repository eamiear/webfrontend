# CommonJS

>关于`CommonJS`的介绍和使用  
>`CommonJS`遵循`CMD`规范  
>`CMD`很多特性面向服务器端,无法再客户端/浏览器实现——比如`io`、`system`等。  
>`CMD`模块只能定义对象。  


####**特点**
 - 一个`CJS`模块是一段可复用的`Javascript`,它导入一些列特定的对象给依赖它的代码调用(没有`define`函数包裹)。
 - `CJS`有一个`exports`变量，用于向其它模块提供对象。  
 - 还有一个`require`函数,用于引用其它依赖模块。  


<br>
####**使用** 

#####**`require()`与`exports`**

```
// package/lib 是依赖模块/文件
var lib = require('package/lib');
 
function foo(){
    lib.log('hello world!');
}
 
// 把 foo 暴露给其它模块
exports.foo = foo;

```

#####**`exports`的使用**

>模块定义

```
//构造函数，包含一些属性或方法
function foobar(){
        this.foo = function(){
                console.log('Hello foo');
        }
 
        this.bar = function(){
                console.log('Hello bar');
        }
}
 
// 把 foobar 暴露给其它模块
exports.foobar = foobar;
 
```
>模块使用  

```
// 当前文件与模块文件在同一目录路
var foobar = require('./foobar').foobar,
    test   = new foobar();
 
test.bar(); // 'Hello bar'

```
<br>
#####**使用`AMD`定义模块**

```
define(['package/lib'], function(lib){
 
    function foo(){
        lib.log('hello world!');
    } 
 
    // 把 foo 暴露给其它模块
    return {
        foobar: foo
    };
});
```
<br>
#####**使用多个依赖模块**

`app.js`

```
var modA = require('./foo');
var modB = require('./bar');
 
exports.app = function(){
    console.log('Im an application!');
}
 
exports.foo = function(){
    return modA.helloWorld();
}
```

`bar.js`

```
exports.name = 'bar';

```

`foo.js`

```
require('./bar');
exports.helloWorld = function(){
    return 'Hello World!!''
}
```
