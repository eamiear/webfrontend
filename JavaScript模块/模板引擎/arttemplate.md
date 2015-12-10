# artTemplate
> `<script type="text/html"></script>`标签来存放模板（由于浏览器不支持这种类型的声明，它存放的代码不会当作 `js `运行，代码也不会被显示出来）


####**创建模板**
使用一个type="text/html"的script标签存放模板：
```
<script id="test" type="text/html">
<h1>{{title}}</h1>
<ul>
    {{each list as value i}}
        <li>索引 {{i + 1}} ：{{value}}</li>
    {{/each}}
</ul>
</script>

```
####**渲染模板**

```
var data = {
    title: '标签',
    list: ['文艺', '博客', '摄影', '电影', '民谣', '旅行', '吉他']
};
var html = template('test', data);
document.getElementById('content').innerHTML = html;
```

####**方法**

`template(id, data)`

> 根据 `id `渲染模板。内部会根据`document.getElementById(id)`查找模板。

> 如果没有` data `参数，那么将返回一渲染函数。

`template.compile(source, options)`

> 将返回一个渲染函数。演示

`template.render(source, options)`

> 将返回渲染结果。

`template.helper(name, callback)`

> 添加辅助方法。

>例如时间格式器：演示

`template.config(name, value)`

>更改引擎的默认配置。

| 字段 | 类型 | 默认值 | 说明 |
| -- | -- | -- | -- |
|`openTag` | `String`| `{{`| 逻辑语法开始标签 |
|`closeTag`| `String`| `}}`| 逻辑语法结束标签|
|` escape` |`Boolean`| true| 是否编码输出 HTML 字符 |
|` cache ` |`Boolean`| true| 是否开启缓存（依赖 options 的 filename 字段） |
|`compress`|`Boolean`| false| 是否压缩 HTML 多余空白字符 |

<br>

```
<html>
<head>
<meta charset="UTF-8">
<title>compile-demo</title>
<script src="../dist/template.js"></script>
</head>

<body style="zoom: 1;">
<h1>在javascript中存放模板</h1>
<div id="content"><ul><li>索引 1 ：摄影</li><li>索引 2 ：电影</li><li>索引 3 ：民谣</li><li>索引 4 ：旅行</li><li>索引 5 ：吉他</li></ul></div>

<script>
    var source = '<ul>'
    +    '{{each list as value i}}'
    +        '<li>索引 {{i + 1}} ：{{value}}</li>'
    +    '{{/each}}'
    + '</ul>';
    
    var render = template.compile(source);
    var html = render({
        list: ['摄影', '电影', '民谣', '旅行', '吉他']
    });
    
    document.getElementById('content').innerHTML = html;
</script>

</body>
</html>

```

```
<html>
<head>
<meta charset="UTF-8">
<title>basic-demo</title>
<script src="../dist/template.js"></script>
</head>

<body style="zoom: 1;">
<div id="content">

<h1>基本例子</h1>
<ul>
    <li>索引 1 ：文艺</li>
    <li>索引 2 ：博客</li>
    <li>索引 3 ：摄影</li>
    <li>索引 4 ：电影</li>
    <li>索引 5 ：民谣</li>
    <li>索引 6 ：旅行</li>
    <li>索引 7 ：吉他</li>
</ul>

</div>

<script id="test" type="text/html">
    {{if isAdmin}}
        <h1>{{title}}</h1>
        <ul>
            {{each list as value i}}
                <li>索引 {{i + 1}} ：{{value}}</li>
            {{/each}}
        </ul>
    {{/if}}
</script>

<script>
var data = {
	title: '基本例子',
	isAdmin: true,
	list: ['文艺', '博客', '摄影', '电影', '民谣', '旅行', '吉他']
};
var html = template('test', data);
document.getElementById('content').innerHTML = html;
</script>

</body></html>
```
<br>

#####**阅读**
- [artTemplate](http://aui.github.io/artTemplate/)
- [artTemplate 简洁语法版](https://github.com/aui/artTemplate/wiki/syntax:simple)