# jQuery插件开发指南
** [原文链接](https://github.com/peterkokot/awesome-jquery/blob/master/CONTRIBUTING.md) **

**开发jQuery插件的最佳实践**


在开发jQuery插件的过程之中，并没有所谓的权威指南。
以下是一些来自 [官方文档](http://learn.jquery.com/plugins/) 的**最佳实践**。

* [1. 稳固：保护作用域内的 $ 免受污染](#tip-1)
* [2. 发布：使用包管理器](#tip-2)
* [3. 维护：维护你的插件，并坚持下去](#tip-3)
* [4. 配置：提供默认的配置](#tip-4)
* [5. 文档](#tip-5)
* [6. 测试](#tip-6)
* [7. 协作：和其他插件协同工作](#tip-7)
* [8. 易用](#tip-8)


## 1. 稳固：保护作用域内的 $ 免受污染<a name="tip-1"></a>

由于其他库或者框架也可能使用了 $ 做为他们的别名(*译者注：比如zepto,prototype*)，
所以插件的外部应该使用一个闭包函数包裹起来，
并把jQuery做为参数传入，
以保证作用域中的 $ 是属于jQuery的。

```javascript
(function($) {
    // code here can use $ to reference jQuery
})(jQuery);
```

## 2. 发布：使用包管理器<a name="tip-2"></a>

JavaScript拥有 **一大票** 的 包管理器 (npm, Bower, component, spm, jam, jspm, Ender, volo, Duo)。
鉴于目前前端er都在使用包管理器，所以还是有必要让你的jQuery插件提供对包管理器支持。
这里建议使用`npm`，因为连jQuery也托付给了它。
第二推荐的是`Bower`，因为它用户群体大,而且使用方便(*译者注：Bower已经停止维护了*)。


## 3. 维护：维护你的插件，并坚持下去<a name="tip-3"></a>
将呕心沥血的开发jQuery插件贡献给开源的jQuery社区，是一件光荣的事情。
然后开源会让插件中一些bug提前暴露出来，
因此持之以恒的接受来自GitHub的PR，或是修复bug，或是针对最新版本jQuery添加支持，都是必要的。

## 4. 配置：提供默认的配置<a name="tip-5"></a>

大多数的插件都需要一些配置. 在用户没有进行配置时，插件应该自动使用默认值.

```javascript
$("#select").myPlugin({mode: 'brush', lineWidth: 3, color: '#c3c3c3'});
```

```javascript
var defaultSettings = {
    mode            : 'Pencil',
    lineWidth       : 2,
    color 			: '#ff0000'
};
```

## 5. 文档<a name="tip-6"></a>

通常在编译代码时，头部会添加一些有意义的东西（文档），
是为了更好的区分开readme文件和doc文件，
有利于人们更好的读懂你的文件和代码

## 6. 测试<a name="tip-7"></a>

在多个浏览器中测试你的插件


## 7. 协作：和其他插件协同工作

当你的插件不需要返回值时，请确保末尾返回自身

```javascript
return this;
```

这样可以让你的插件、我的插件、他们的插件以链式调用的方式串起来(译者脑补：`串一株幸运草，串一个同心圆..`)

```javascript
$("div#myid").yourPlugin().anotherPlugin().yetAnotherPlugin();
```

## 8. 易用

在不阅读文档、进行配置或者改动插件代码的情形下，插件也应该是能立即使用的。

如果可能的话，确保插件可以自行初始化:

```html
<div class="mySliderPlugin"></div>
```

不需要增加或者改动代码:

```javascript
$('.mySliderPlugin').mySliderPlugin();
```

插件能够自主完成初始化:

```javascript
$(function() {
    $(".myjqWidget").myjqWidget();
});
```
