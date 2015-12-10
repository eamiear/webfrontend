# MV* Patterns

>关于MVC模式、MVP模式、MVVM模式的介绍


#####**`MV*`的比较**
- `MVP`和`MVVM`都是`MVC`的衍生。`MVC`与衍生模式的区别在于每层都依赖其他层及它们间的紧密程度。

- 在`MVC`中，它的结构是这样的：`View`-->`Controoller`-->`Model`.所以`View`层知晓`Controller`层,`Controller`层知晓`Model`层。`MVC`中，`View`可以直接访问`Model`层，将`Model`层完全暴露给`View`,可能存在安全和性能的成本，取决于项目的复杂程度，而`MVVM`则避免了这些问题。

- 在`MVP`中，`Controller`由`Presenter`代替。它监听来自`View`和`Model`的事件并协调它们间的操作。与`MVVVM`不同，它没有`View`和`ViewModel`的绑定机制，所以依赖`View`通过实现接口来实现`Presenter`与`View`的交互。

- `MVVM`允许创建特定的`View`的`Model`子集,这些子集里可以包含状态和逻辑信息，避免向`View`暴露整个`Model`.与`MVP`的`Presenter`不同的是，一个`ViewModel`不需要引用`View`，`View`可以与`ViewModel`中的属性绑定，相应的这些属性将包含的数据暴露给`View`。这样`View`中的逻辑就非常少了。其中一个缺点是，每层的解读都需要在`ViewModel`和`View`中进行，这个存在一定性能损耗(成本).而`MVC`不存在这个问题。

<br>
#####**阅读**
- [MVC，MVP 和 MVVM 的图示](http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html)
- [Scaling Isomorphic Javascript Code](http://blog.nodejitsu.com/scaling-isomorphic-javascript-code/)
- [Understanding MVC, MVP and MVVM Design Patterns](http://www.dotnet-tricks.com/Tutorial/designpatterns/2FMM060314-Understanding-MVC,-MVP-and-MVVM-Design-Patterns.html)
- [MVC vs. MVP vs. MVVM](http://kb.cnblogs.com/page/120678/)
- [MVC vs. MVP vs. MVVM](https://nirajrules.wordpress.com/2009/07/18/mvc-vs-mvp-vs-mvvm/)
- [MVC Versus MVP Versus MVVM](https://www.safaribooksonline.com/library/view/learning-javascript-design/9781449334840/ch10s09.html)