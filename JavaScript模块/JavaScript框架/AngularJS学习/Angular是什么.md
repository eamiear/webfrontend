# Angular是什么

#####**简介**
`AngularJS`是一个开发动态`web`应用的框架。它让你可以使用 `HTML`作为模板语言(`ng-repeat`)，并且可以通过扩展的`HTML`语法来使应用组件更加清晰和简洁。  
它的创新之处在于，通过数据绑定和依赖注入减少了大量代码，而这些都在浏览器端通过`JavaScript`实现，能够和任何服务器端技术完美结合。

`Angular`是为了扩展HTML在构建应用时本应具备的能力而设计的。对于静态文档，`HTML`是一门很好的声明式的语言，但对于构建动态`WEB`应用，它无能为力。所以，构建动态WEB应用往往需要一些技巧才能让浏览器配合我们的工作。

通常，我们通过以下手段来解决动态应用和静态文档之间不匹配的问题：

- 类库 - 一些在开发WEB应用时非常有用的函数的集合。你的代码起主导作用，并且决定何时调用类库的方法。例如：`jQuery`等。
- 框架 - 一种`WEB`应用的特殊实现，你的代码只需要填充一些具体信息。框架起主导作用，并且决定何时调用你的代码。例如：`knockout, ember`等。

`Angular`尝试去扩展`HTML`的结构来弥合以文档为中心的`HTML`与实际`Web`应用所需要的`HTML`之间的鸿沟。`Angular`通过指令`（directive）`扩展`HTML`的语法。

#####**AngularJS的特点**
- 构建一个`CRUD`应用时可能用到的所有技术：数据绑定、基本模板指令、表单验证、路由、深度链接、组件重用、依赖注入。
- 可测试性：单元测试、端到端测试、模拟对象（`mocks`）、测试工具。
- 拥有一定目录结构和测试脚本的种子应用。


#####**AngularJS的使用场合**
`Angular`并不是适合任何应用的开发(高层次的抽象来简化应用的开发,损失灵活性)，**`Angular`主要用于构建`CRUD`应用**。（大多数`WEB`应用都是`CRUD`应用）

对于像游戏和有图形界面的编辑器之类的应用，会进行频繁且复杂的`DOM`操作，不适合用`Angular`来构建。在这种场景下，使用更低抽象层次的类库可能会更好，例如：`jQuery`。

#####**AngularJS的主要核心特性**
- **模板**(`Template`)： 带有`Angular`扩展标记的`HTML`
- **指令**(`Directive`)： 用于通过自定义属性和元素扩展`HTML`的行为
- **模型**(`Model`)：用于显示给用户并且与用户互动的数据
- **作用域**(`Scope`)： 用来存储模型(`Model`)的语境(`content`上下文)。模型放在这个语境中才能被控制器，指令和表达式等访问到
- **表达式**(`Expression`)：模板中可以通过它来访问作用(`Scope`)中的变量和函数
- **编译器**(`Compiler`)：用来编译模板（`Template`）,并且对其中包含的指令和表达式进行实例化
- **过滤器**（`Filter`）：负责格式化表达式的值，以便呈现给用户
- **视图**（`View`）：用户看到的内容（`DOM`）
- **数据绑定**（`Data Binding`）：自动同步模型中的数据和视图的表现
- **依赖注入**（`Dependency Injection`）：负责创建和自动装载对象或函数
- **注入器**（`Injector`）：用来实现依赖注入的容器
- **模块**（`Module`）：用来配置注入器
- **服务**（`Service`）：独立于视图的、可复用的业务逻辑

<br>
#####**AngularJS的使用**
```
<!DOCTYPE HTML>
<html>
<head>
	<title></title>
	<meta charset="utf-8">
	<script src="scripts/angular.min.js"></script>
</head>
<body>
<div ng-app="" ng-init="name='World'">
   Hello {{ name }}！
</div>  	
</body>
</html>
```
1. `ng-app`：`ng-app`指令用来标明一个`AngularJS`应用程序，并通过`AngularJS`完成自动初始化应用和标记应用根作用域，同时载入和指令内容相关的模块，并通过拥有`ng-app`指令的标签为根节点开始编译其中的`DOM`。  
简单地说，`ng-app`指明某个标签（元素/块）为`AngularJS`程序，并作为程序的入口。  
`<html ng-app>`表示整个页面都是`angular`应用程序，否则，页面中指定`ng-app`的部分是`angular`应用程序。  
在任何一个单页面中`ng-app`只能出现一次，`ng-app`相当于`c`语言中的`main`函数，制定`Angular`的作用范围。
2. `ng-init`：数据初始化
3. ![表达式](表达式.png)：表达式，显示数据

######**渲染流程**
- 浏览器启动加载页面，解析、渲染页面（包括在`DOM`上定义的指令属性或方法）
- `AngularJS`启动，编译器遍历`DOM`树来解析`HTML`，寻找这些指令属性、函数，在一个`DOM`元素上找到一个或多个这样的指令属性函数，它们就会被收集起来、排序，然后按照优先级顺序被执行。
- 页面显示`AngularJS`模板渲染的数据。

上面通过表达式进行数据绑定存在一些问题，在页面渲染过程中，`AngularJS`未对`DOM`树进行解析渲染，这样页面中会出现未被渲染的模板`{{ name }}`，这种情况可以使用`ng-bind`指令来避免。
`ng-bind`在`angular`解析渲染完毕后才将数据显示出来，而表达式`{{}}`在`angular`解析渲染到它时就显示数据。

<br>
#####**阅读**
-  [什么是Angular？](http://docs.ngnice.com/guide/introduction)
-  [Angular 概述 ](http://docs.ngnice.com/guide/concepts#template)
-  [AngularJS](http://www.hubwiz.com/class/547c3e3b88dba0087c55b4e5)