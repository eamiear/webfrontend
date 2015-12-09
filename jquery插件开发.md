# jQuery插件开发

#####**1. 创建一个基础插件**

**$$插件的意义：$$** 通过`jQuery`选择器调用插件中一个或多个方法，以对该选择器进行一系列操作。插件的好处在于能够在代码中复用。


#####**2. jQuery工作机制：jQuery对象方法**

```
$( "a" ).css( "color", "red" );
```
当使用`$`函数来选择元素时，将返回一个`jQuery`对象。这个对象包含了所有`jQuery`提供的方法及所有匹配该选择器的元素。这些`jQuery`方法都来自于`$.fn`对象，这个对象包含了所有`jQuery`对象方法，所以，如果我们想自定义方法，则在该对象上定义即可。


#####**3. 编写基础插件**

```
$.fn.greenify = function() {
    this.css( "color", "green" );
};
```

```
$( "a" ).greenify(); // Makes all the links green.
```

#####**4. 支持链式**

在所有`jQuery`对象方法中都返回一个初始的`jQuery`对象，可以实现`jQuery`的链式特性。

```
$.fn.greenify = function() {
    this.css( "color", "green" );
    return this;
}
```
```
$( "a" ).greenify().addClass( "greenified" );
```
 
#####**5. 保护`$`别名并添加作用域**

在代码开发中，如果需要使用多个`Javascript`库，就存在命名冲突的情况。`jQuery`中可以通过`jquery.noConflict()`方法来取消对`$`别名的使用，但对于很多以`$`别名的插件，则会产生影响。可以通过立即执行函数解决这个问题。如下：

```
(function ( $ ) {
 
    $.fn.greenify = function() {
        this.css( "color", "green" );
        return this;
    };
 
}( jQuery ));
```

即定义一个以`$`命名参数的函数，并立即执行且以`jQuery`对象作为参数。

**`NOTE`：** 立即执行函数的最初目的是，允许函数包含私有变量。

```
(function ( $ ) {
 
    var shade = "#556b2f";
 
    $.fn.greenify = function() {
        this.css( "color", shade );
        return this;
    };
 
}( jQuery ));
```


#####**	6. 最小化插件**

一般情况下，一个插件最好就包含一个`$.fn`对象：减少你的插件被其他插件覆盖或覆盖其他插件的可能性。不提倡下面的写法：

```
(function( $ ) {
 
    $.fn.openPopup = function() {
        // Open popup code.
    };
 
    $.fn.closePopup = function() {
        // Close popup code.
    };
 
}( jQuery ));
```

比较好的方式。

```
(function( $ ) {
 
    $.fn.popup = function( action ) {
 
        if ( action === "open") {
            // Open popup code.
        }
 
        if ( action === "close" ) {
            // Close popup code.
        }
 
    };
 
}( jQuery ));
```

#####**7. 使用each()方法**

`jQuery`对象一般都是元素的集合。如果需要对集合中的任意元素或特定元素进行操作，可以使用`.each()`来循环元素。

```
$.fn.myNewPlugin = function() {
 
    return this.each(function() {
        // Do something to each element here.
    });
 
};
```

**`NOTE`：**这里没有返回`this`对象，而是直接返回了`each()`。因为`.each()`也是链式性的，它返回`this`。所以这里直接返回`each()`，实际上也是返回了`this`


#####**	8. 接收参数**

当插件相对复杂时，对插件进行自定义配置尤为必要。

```

(function ( $ ) {
 
    $.fn.greenify = function( options ) {
 
        // This is the easiest way to have default options.
        var settings = $.extend({
            // These are the defaults.
            color: "#556b2f",
            backgroundColor: "white"
        }, options );
 
        // Greenify the collection based on the settings variable.
        return this.css({
            color: settings.color,
            backgroundColor: settings.backgroundColor
        });
 
    };
 
}( jQuery ));
```
使用示例：

```
$( "div" ).greenify({
    color: "orange"
});
```

#####**9. 将上述讨论进行整合**

```
(function( $ ) {
 
    $.fn.showLinkLocation = function() {
 
        this.filter( "a" ).each(function() {
            var link = $( this );
            link.append( " (" + link.attr( "href" ) + ")" );
        });
 
        return this;
 
    };
 
}( jQuery ));

```
 
```
// Usage example:
$( "a" ).showLinkLocation();

```

`HTML`代码

```
<!-- Before plugin is called: -->
<a href="page.html">Foo</a>
 
<!-- After plugin is called: -->
<a href="page.html">Foo (page.html)</a>

```

代码优化如下

```
(function( $ ) {
 
    $.fn.showLinkLocation = function() {
 
        this.filter( "a" ).append(function() {
            return " (" + this.href + ")";
        });
 
        return this;
 
    };
 
}( jQuery ));
```


#####**阅读**
[jQuery插件开发](http://learn.jquery.com/plugins/basic-plugin-creation/)