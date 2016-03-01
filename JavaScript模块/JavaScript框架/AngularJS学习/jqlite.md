# jqLite

`AngularJS`中，如果想像`jQuery`那样对`DOM`进行操作，可以使用`jqLite`。

`jqLite`以`angular.element`接口提供出来，不支持选择符，与`jQuery`一样兼容多个浏览器。

使用示例：

```javascript
var tpl = document.querySelector('#clock');
angular.element(tpl).text(...);
```

其他方法查看`API`

[angular.element](http://docs.ngnice.com/api/ng/function/angular.element)