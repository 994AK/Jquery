
我们得出编写一个jQuery插件的原则：
- 给$.fn绑定函数，实现插件的代码逻辑；
- 插件函数最后要return this;以支持链式调用；
- 插件函数要有默认值，绑定在$.fn.<pluginName>.defaults上；
- 用户在调用时可传入设定值以便覆盖默认值。

```js
//写着重复代码...应该用代码自定义封装
      
// $('#box p').css('backgroundColor', '#fffceb').css('color', '#d85939');
// $('#box2 p').css('backgroundColor', '#fffceb').css('color', '#d85939');

//为了改变上面重复调用我们可以使用 $.fn进行绑定函数
$.fn.highlight1 = function () {
    //this已经绑定为当前JQuery对象；
    this.css('backgroundColor', '#fffceb').css('color', '#d85939');
    return this;
}

$('#box p').highlight1();
$('#box2 p ').highlight1();
```

当然上面的封装没有自定义功能，让用户自己添加属性
```js
//为了用户体验，让用户自己添加颜色
$.fn.highlight2 = function (options) {
    //要考虑到各种情况;
    //options 为undefined
    //options 只有部分key
    var bgcolor = options && options.backgroundColor || '#fffceb';
    var color = options && options.color || '#d85030';
    this.css('backgroundColor', bgcolor).css('color', color);
    return this;
}

//设置初始值
$('#test-highlight2 span').highlight2({
    backgroundColor:'#00a8e6',
    color:'#fff'
})
```

还可以优化成一行完成的代码,需要调用$.extend方法，它把多个object对象的和属性合并到第一个target对象中

```js
$.fn.highlight = function (options) {
    //合并默认值和用户设定值
    var opts = $.extend({},$.fn.highlight.defaults,options);
    this.css('backgroundColor',opts.backgroundColor).css('color',opts.color);
    return this
}
//设定默认值
$.fn.highlight.default = {
    color:'#d85030',
    backgroundColor:'#fff8de'
}
//用户输入
$.fn.highlight.default.color = '#fff';
$.fn.highlight.default.backgroundColor = '#000'

```
