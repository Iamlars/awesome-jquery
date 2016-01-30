# jQuery插件开发指南
** [原文链接](https://github.com/peterkokot/awesome-jquery) **

**开发jQuery插件的最佳实践**


在开发jQuery插件的过程之中，并没有所谓的权威指南。
以下是一些来自 [官方文档](http://learn.jquery.com/plugins/) 的**最佳实践**。

* [1. 稳固：保护作用域内的 $ 免受污染](#tip-1)
* [2. 发布：使用包管理器](#tip-2)
* [3. 维护：维护你的插件，并坚持下去](#tip-3)
* [4. 设置：提供默认的设置](#tip-4)
* [5. 文档](#tip-5)
* [6. 测试](#tip-6)
* [7. 协作：和其他插件协同工作](#tip-7)
* [8. 态度：不高冷](#tip-8)


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

## 4. 设置：提供默认的设置<a name="tip-5"></a>

Plugins in most cases have some configuration. If user don't set these plugin should have set default values for easier and faster plugin implementation.

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

## 5. Documentation<a name="tip-6"></a>

Always document your code by adding meaningful concise comments to the top of the plugin file and in cases of complex plugins creating separate `README` file or `doc` folder with deep explanations and demostration of the plugin. This helps people understand and use your plugin better.


## 6. Testing<a name="tip-7"></a>

Test your plugin in multiple browser.


## 7. Enable chaining

Unless your plugin returns a value, the last line of your plugin function should be:

```javascript
return this;
```

this enables chaining of method calls:

```javascript
$("div#myid").yourPlugin().anotherPlugin().yetAnotherPlugin();
```

## 8. Easy Usage

Plugin should be easy to use and should work out of the box withouth the need to browse the documentation, set options or editing plugin code.

If possible make sure that plugin can initialize itself:

```html
<div class="mySliderPlugin"></div>
```

without the need to add or edit any JavaScript:

```javascript
$('.mySliderPlugin').mySliderPlugin();
```

Plugin can initialize itself:

```javascript
$(function() {
    $(".myjqWidget").myjqWidget();
});
```
