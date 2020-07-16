操作DOM
 
```js
.html()//修改DOM节点的HTML
.text()//修改DOM节点的文本

//修改CSS
.css(CSS,元素)//修改css的样式
.hasClass(Class)//检查DOM节点的Class上有没有这个属性
.addClass(Class)//添加Class的元素
.removeClass(Class) //删除Class的元素

//disabled属性
.hide()//隐藏
.show()//显示

//检查浏览器目前的高度/某个盒子的高度
.width()//高度
.height()//可视的高度

.attr(属性,修改属性) //检查DOM节点标签自带属性 比如 name，start，ID等..
.removeAttr(属性) // 删除DOM节点自带的属性 比如 name......
.prop('属性名称','true/false') //比如用来判断选中复选框为true，没选中为false
.val()//修改input的value属性
```
案例
```html
<!--练习val属性-->
<input id="test-input" name="email" value="">
<select id="test-select" name="city">
    <option value="BJ" selected>Beijing</option>
    <option value="SH">Shanghai</option>
    <option value="SZ">Shenzhen</option>
</select>
<textarea id="test-textarea">Hello</textarea>
```

```js
    //val()方法获取和设置对应的value属性
    var input = $('input[name=email]'),
        select = $('select[name=city]'),
        textarea=$('#test-textarea');

    input.val();//'test'
    input.val('abc') //文本框的内容已经修改为abc

    select.val()//'BJ' 默认的是BJ选择
    select.val('SH'); // 选择框已变为Shanghai

    textarea.val();//'Hello'
    textarea.val('Hi');//文本框区域已经更新为'Hi'


```
修改DOM结构

```js
.append()添加DOM往后面添加
.prepend()添加DOM往最前添加
.after()某个节点插入指定的位置
.remove()删除节点
```

案例
```html
 <div id="test-div">
        <ul>
            <li><span>JavaScript</span></li>
            <li><span>Python</span></li>
            <li><span>Swift</span></li>
        </ul>
    </div>
```
```js
//请再添加Pascal、Lua和Ruby，然后按字母顺序排序节点：
var ul = $('#test-div ul');
var languages = ['Pascal','Lua','Ruby'];
languages.map(lang=>ul.append('<li><span>'+lang+'<span></li>'))
var lis = ul.find('li');
lis.sort((li1,li2)=>li1.innerHTML < li2.innerHTML ?-1 : 1);
ul.append(lis);

```