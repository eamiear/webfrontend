# 模板引擎

#####**模板语法**

- “嵌入式”：可以将`js`直接写在模板里面，从而实现一些复杂的渲染逻辑。
- “无逻辑(`Logic-less`)”：模板与逻辑尽可能分离，一般只包含简单的逻辑或无逻辑。(`mustache`)  


<br>
#####**模板引擎的作用**

######**原始方式:**
 
```
    /**
     * 模板构建函数
     *
	 * 构建轮播图列表模板
	 * @param item 数据对象
	 */
	var _buildSliderList = function(item){
		if(item==null) return "";
		var liTpl = '';
		liTpl += '<div><img src="'
			 // + App.PIC_URL_PRE
			 // + item.firstPicUrl
			  + item.picUrl
			  + '" data-id="'
			  + item.id
			  + '" onerror="this.src=\''
			  + contextPath
			  + '/resources/images/city/city.jpg\'"' 
			  + ' alt="top-image" style="width:100%;height:100%;"/><div class="pic-title"><div>'
			  + item.title
			  + '</div></div></div>';
		return liTpl;
	}
```
> UI与逻辑代码混杂在一起,不便于阅读；对于简单的页面，简单的拼接`HTML`字符串比较灵活，但对于较为复杂的业务或多人维护的情况下，很容易出现问题.  

<br>
####**`artTemplate`**:
```
<script id="tmpl" type="text/html">
{{each topData as vo}}
    <img src="{{vo.picUrl}}" data-id="{{vo.id }}" style="width:100%;height: 100%;">
    
    <div class="pic-title">
		<div>{{vo.title}}</div>
	</div>
{{/each}}
</script>

```
> 使用模板引擎，提高了前端模块的编写、修改和阅读

  
<br>
#####**嵌入式与无逻辑(`Logic-less`)**

######**嵌入式(模板内嵌)**:
- 开发调试：如果前端模板不是纯静态页面，则不利于调试，因为调试依赖于服务器(数据)
-   

######**无逻辑(`Logic-less`)**:


<br>
#####**模板引擎的原理**


<br>
#####**编写简单的模板引擎**




<br>
#####**阅读**
- [编写一个简单的JavaScript模板引擎](http://www.liaoxuefeng.com/article/001426512790239f83bfb47b1134b63b09a57548d06e5c5000)
- [JavaScript Micro-Templating](http://ejohn.org/blog/javascript-micro-templating/)
- [JavaScript template engine in just 20 lines](http://krasimirtsonev.com/blog/article/Javascript-template-engine-in-just-20-line)
- [进击！前端模板工程化](https://github.com/aui/tmodjs/blob/master/doc/why-tmodjs.md)