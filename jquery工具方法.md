# jQuery工具方法

####**1.`$.trim`  **
`$.trim`方法用于移除字符串头部和尾部多余的空格。   

```
$.trim("  hello, how are you?  ");

//"hello, how are you?"

```
####**2.`$.contains` ** 
`$.contains`方法返回一个布尔值，表示某个DOM元素（第二个参数）是否为另一个DOM元素（第一个参数）的下级元素。  

```
jQuery.contains(document.documentElement, document.body); // true
jQuery.contains(document.body, document.documentElement); // false
```
####**3.` $.each，$.map`  **
`$.each`方法用于遍历数组和对象，然后返回原始对象。它接受两个参数，分别是数据集合和回调函数(每个成员/元素执行的回调函数)。

```
$.each([ 52, 97 ], function( index, value ) {
  console.log( index + ": " + value );
});
// 0: 52 
// 1: 97 

var obj = {
  p1: "hello",
  p2: "world"
};
$.each( obj, function( key, value ) {
  console.log( key + ": " + value );
});
// p1: hello
// p2: world
```

`$.map`方法也是用来遍历数组和对象，但是会返回一个新对象。

```
var a = ["a", "b", "c", "d", "e"];
a = $.map(a, function (n, i){
  return (n.toUpperCase() + i);
});
// ["A0", "B1", "C2", "D3", "E4"]

```

####**4.`$.inArray`  **

`$.inArray`方法返回一个值在数组中的位置（从0开始）。如果该值不在数组中，则返回-1。

```
var a = [1,2,3,4];
$.inArray(4,a) // 3
```

####**5.`$.extend`  **

$.extend方法用于将多个对象合并进第一个对象。
```
var o1 = {p1:'a',p2:'b'};
var o2 = {p1:'c'};

$.extend(o1,o2);
o1.p1 // "c"
```

`$.extend`的另一种用法是生成一个新对象，用来继承原有对象。这时，它的第一个参数应该是一个空对象。

```
var o1 = {p1:'a',p2:'b'};
var o2 = {p1:'c'};

var o = $.extend({},o1,o2);
o
// Object {p1: "c", p2: "b"}
```

默认情况下，`extend`方法生成的对象是“浅拷贝”，也就是说，如果某个属性是对象或数组，那么只会生成指向这个对象或数组的指针，而不会复制值。如果想要“深拷贝”，可以在`extend`方法的第一个参数传入布尔值`true`。

```
var o1 = {p1:['a','b']};

var o2 = $.extend({},o1);
var o3 = $.extend(true,{},o1);

o1.p1[0]='c';

o2.p1 // ["c", "b"]
o3.p1 // ["a", "b"]
```
上面代码中，o2是浅拷贝，o3是深拷贝。结果，改变原始数组的属性，o2会跟着一起变，而o3不会。

####**6. `$.proxy`  **  

`$.proxy`方法类似于`ECMAScript 5`的`bind`方法，可以绑定函数的上下文（也就是`this`对象）和参数，返回一个新函数。  
`jQuery.proxy()`的主要用处是为回调函数绑定上下文对象。

```
var o = {
    type: "object",
    test: function(event) {
        console.log(this.type);
    }
};

$("#button")
  .on("click", o.test)
  .on("click", $.proxy(o.test, o)) // object
```

上面的代码中，第一个回调函数没有绑定上下文，所以结果为空，没有任何输出；第二个回调函数将上下文绑定为对象o，结果就为object。

这个例子的另一种等价的写法是：

```
$("#button").on( "click", $.proxy(o, test))
```

上面代码的`$.proxy(o, test)`的意思是，将`o`的方法`test`与`o`绑定。

这个例子表明，`proxy`方法的写法主要有两种。

```
jQuery.proxy(function, context)

// or

jQuery.proxy(context, name)
```

第一种写法是为函数（`function`）指定上下文对象（`context`），第二种写法是指定上下文对象（`context`）和它的某个方法名（`name`）。

再看一个例子。正常情况下，下面代码中的this对象指向发生`click`事件的`DOM`对象。

```
$('#myElement').click(function() {
    $(this).addClass('aNewClass');
});
```

如果我们想让回调函数延迟运行，使用`setTimeout`方法，代码就会出错，因为`setTimeout`使得回调函数在全局环境运行，`this`将指向全局对象。

```
$('#myElement').click(function() {
    setTimeout(function() {
        $(this).addClass('aNewClass');
    }, 1000);
});
```

上面代码中的`this`，将指向全局对象`window`，导致出错。

这时，就可以用`proxy`方法，将`this`对象绑定到`myElement`对象。

```
$('#myElement').click(function() {
    setTimeout($.proxy(function() {
        $(this).addClass('aNewClass'); 
    }, this), 1000);
});
```

####**7. `$.data，$.removeData`  ** 
`$.data`方法可以用来在`DOM`节点上储存数据。

```
// 存入数据
$.data(document.body, "foo", 52 );

// 读取数据
$.data(document.body, "foo");

// 读取所有数据
$.data(document.body);
```

上面代码在网页元素`body`上储存了一个键值对，键名为`“foo”`，键值为`52`。

`$.removeData`方法用于移除`$.data`方法所储存的数据。

```
$.data(div, "test1", "VALUE-1");
$.removeData(div, "test1");
```

####**8. `$.parseHTML，$.parseJSON，$.parseXML`**

`$.parseHTML`方法用于将字符串解析为`DOM`对象。

`$.parseJSON`方法用于将`JSON`字符串解析为`JavaScript`对象，作用与原生的`JSON.parse()`类似。但是，jQuery没有提供类似`JSON.stringify()`的方法，即不提供将JavaScript对象转为`JSON`对象的方法。

`$.parseXML`方法用于将字符串解析为`XML`对象。

```
var html = $.parseHTML("hello, <b>my name is</b> jQuery.");
var obj = $.parseJSON('{"name": "John"}');

var xml = "<rss version='2.0'><channel><title>RSS Title</title></channel></rss>";
var xmlDoc = $.parseXML(xml);
```

####**9. `$.makeArray `**

`$.makeArray`方法将一个类似数组的对象，转化为真正的数组。

```
var a = $.makeArray(document.getElementsByTagName("div"));
```


####**10 `$.merge`**

`$.merge`方法用于将一个数组（第二个参数）合并到另一个数组（第一个参数）之中。

```
var a1 = [0,1,2];
var a2 = [2,3,4];
$.merge(a1, a2);

a1
// [0, 1, 2, 2, 3, 4]
```

####**11 `$.now`**

`$.now`方法返回当前时间距离1970年1月1日00:00:00 UTC对应的毫秒数，等同于`(new Date).getTime()`。

```
$.now()
// 1388212221489
```

<br>
- [JavaScript标准参考教材](http://javascript.ruanyifeng.com/jquery/utility.html#toc0)