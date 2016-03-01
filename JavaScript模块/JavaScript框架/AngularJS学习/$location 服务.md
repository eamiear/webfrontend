#` $location` 服务

` $location` 服务用以解析地址栏中的`URL`，并让你可以访问应用当前路径所对应的路由。它同样提供了修改路径和处理各种形式导航的能力。  
` $location`服务是对`Javascript`中的`window.location`的进一步封装，但它没有刷新整个页面的能力。刷新页面操作需要使用`$window.location`对象（`window.location`的一个接口）。

* `path()`
> `path()`用来获取页面当前的路径：  
> ```
$location.path();//返回当前路径
> ```
>修改当前路径并跳转到应用中的另一个`URL`：
> ```
$location.path('/');//把路径修改为'/'路由
> ```

* `replace()`
>如果你希望跳转后用户不能点击后退按钮（对于登录之后的跳转这种发生在某个跳转之后的再次跳转很有用），`AngularJS`提供了`replace()` 方法来实现这个功能：
> ```javascript
$location.path('/home');
$location.replace();
// 或者
$location.path('/home').replace();
>```

* `absUrl()`
> `absUrl() `方法用来获取编码后的完整`URL`：
> ```
$location.absUrl()
>```

* `hash()`
> `hash() `方法用来获取`URL`中的`hash`片段：
> ```
$location.hash()
>```

* `host()`
> `host() ` 方法用来获取`URL`中的主机：
> ```
$location.host()
>```

* `port()`
> `port() ` 方法用来获取`URL`中的端口号：
> ```
$location.port()
>```

* `protocol()`
> `protocol() `方法用来获取`URL`中的协议：
> ```
$location.protocol()
>```


* `search()`
> `search() `方法用来获取`URL`中的查询串：
> ```
$location.search()
>```
>我们可以向这个方法中传入新的查询参数，来修改`URL`中的查询串部分：
> ```javascript
// 用对象设置查询
$location.search({name: 'Ari', username: 'auser'});
// 用字符串设置查询
$location.search('name=Ari&username=auser');
> ```
>`search`方法可以接受两个参数。
> * `search`（可选，字符串或对象）  
这个参数代表新的查询参数。 `hash`对象的值可以是数组。
> * `paramValue`（可选，字符串）  
如果`search`参数的类型是字符串，那么`paramValue`会做为该参数的值覆盖`URL`当中的对应
值。如果`paramValue`的值是`null `，对应的参数会被移除掉。


* `url()`
> `url() `方法用来获取当前页面的`URL`：
> ```
$location.url(); // 该URL的字符串
>```
>我们可以向这个方法中传入新的查询参数，来修改`URL`中的查询串部分：

>如果调用`url()` 方法时传了参数，会设置并修改当前的`URL`，这会同时修改`URL`中的路径、
查询串和`hash`，并返回`$location`。
> ```javascript
// 设置新的URL
$location.url('/home?name=Ari#hashthing');
>```
>`url() `方法可以接受两个参数。
> * `url `（可选，字符串） :
新的`URL`的基础的前缀。
> * `replace`（可选，字符串） :想要修改成的路径。