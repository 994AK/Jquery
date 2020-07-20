动画效果
>JQ内置的动画 

比如显示与隐藏

- `hide`动画隐藏
- `show`动画显示
- `toggle`方法则根据当前状态决定是show()还是hide()。
- 另外他们还可以接收一个回调函数
```js
var div = $('#test-show-hide');
div.hide(3000);//在3秒内慢慢消失 

div.show(3000);//在3秒内慢慢显示 

div.toggle(3000) //根据他们显示来做相反的操作

//同时他们后面也可以接收一个回调函数
div.hide(3000,function(){})//动画结束后,函数里应该干点什么呢

```
垂直方向展开/收缩
`slideUp` / `slideDown`
 
 - `slideUp` 把一个可见的DOM元素收起，效果跟拉上窗帘一样;
 - `slideDown` 相反
 - `slideToggle()` 根据元素是否可见决定下一步动作
 
 ```js
var div = $('#test-show-hide');
div.slideUp(3000);//在3秒内慢慢消收起
div.slideDown(3000);//在3秒内慢慢显示
```

淡入淡出

 `fadeIn` / `fadeOut`
- `fadIn` 淡出
- `fadeOut`谈入
- `fadeToggle` 根据元素是否可见来决定下一步动作
- `fadeIn`和`fadeOut`的动画效果是淡入淡出,也就是通过不断设置DOM元素的`opacity`实现；


```js
var div = $('#test-show-hide');
div.fadeIn(3000);//在3秒内慢慢淡出显示
div.fadeOut(3000);//在3秒内慢慢淡入消失
```

自定义动画
 
`animate()`自定义动画.

- animate 实现任何动画效果;
- 传入的参数:
   1. DOM元素最终的CSS状态和时间
   2. CSS过渡时间
   3. 回调函数,当动画结束时，该函数将被调用;
 
 ```js
var div = $('#test-show-hide');
//text-btn是点击按钮
$('#text-btn').click(e=>{

  //animate对象的方式添加CSS样式
    div.animate({
        opacity:0.25,
        width:'256px',
        height:'256px',
        backgroundColor:'darkgray'
    },3000,function () {
        console.log('动画结束了');
     
        //动画结束后 执行下面的代码
        $(this).css('opacity','1.0')
                .css('width','128px')
                .css('height','128px')
    });
})
``` 

串行动画

Jq的动画还可以串行执行,通过`delay()`方法还可以实现暂停.

因为动画需要执行一段时间，所以jQuery必须不断返回新的Promise对象才能后续执行操作。简单地把动画封装在函数中是不够的。

```js
var div = $('#test-animates');
// 动画效果：slideDown - 暂停 - 放大 - 暂停 - 缩小
div.slideDown(2000)
   .delay(1000) //暂停一秒
   .animate({
       width: '256px',
       height: '256px'
   }, 2000)
   .delay(1000) //暂停一秒种
   .animate({
       width: '128px',
       height: '128px'
   }, 2000);
}

```

为什么有的动画没有效果

你可能会遇到，有的动画如`slideUp()`根本没有效果。这是因为jQuery动画的原理是逐渐改变CSS的值，如height从100px逐渐变为0。但是很多不是`block`性质的DOM元素，对它们设置`height`根本就不起作用，所以动画也就没有效果。

此外，jQuery也没有实现对`background-color`的动画效果，用`animate()`设置`background-color`也没有效果。这种情况下可以使用CSS3的`transition`实现动画效果。
