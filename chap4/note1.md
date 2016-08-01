#### jQuery中的事件

##### 事件绑定

- bind(type, [data], fn);

> - 参数1：blur, focus, load, resize, scroll, unload, click, dbclick, mousedown, mouseup, mouseover, mousemove, mouseout, mouseenter, mouseleave, change, select, submit, keydown, keypress, keyup, error等
>
> - 参数2：非必选，作为event.data属性值传递给事件对象的额外数据对象
>
> - 参数3：用来绑定的处理函数
>
> ```
> $().bind("click", function(){
>  //...
>});
>//也可以简写
>$().click(function(){
>  //...
>});
> ```
>

- 合成事件

> - hover(enter, leave);
>hover方法准确的说是代替了bind('mouseenter')与bind('mouseleave')，而不是over与out，因此当需要出发hover的第二个方法时，需要使用trigger('mouseleave')
>
>```
>$().hover(function(){
>  //光标进入时发生事件
>},function(){
>  //光标离开时发生事件
>});
>```
>
> - toggle(fn1, fn2, fn3...);
>
>```
>$().toggle(function(){
>  //fn1...
>},function(){
>  //fn2...
>});
>```

##### 事件冒泡

- 事件对象

```
$().bind("click", function(event){
    //...
    event.stopPropagation();  //停止事件冒泡
    event.preventDefault(); //阻止默认行为
});
//可将stopPropagation/preventDefault改写为return false;
```

##### 事件捕获

> 与事件冒泡刚好相反的两个过程，Unfortunately，并不是所有浏览器都支持事件捕获
>
>jQuery不支持事件捕获，可使用JS原生

##### 事件对象的属性

- event.type：获取到事件类型
- event.preventDefault()：阻止默认的事件行为
- event.stopPropagation()：阻止事件的冒泡
- event.target()：获取到触发事件的元素
- event.relatedTarget()：
>对于 mouseover 事件来说，该属性是鼠标指针移到目标节点上时所离开的那个节点。
>对于 mouseout 事件来说，该属性是离开目标时，鼠标指针进入的节点。
>对于其他类型的事件来说，这个属性没有用
- event.pageX / event.pageY：获取光标相对于页面的X坐标和Y坐标
- event.which：获取鼠标的左中右键
- event.metaKey：为键盘事件中获取ctrl按键

##### 移除事件

- unbind([type], [data]);

> 参数1：事件类型
> 参数2：将要移除的函数
>
>```
>$().bind("click", myFun1 = function(){
>  //...
>}).bind("click", myFun2 = function(){
>  //...
>});
>
>$().unbind("click", myFun2);
>```
>

- one(type, [data], fn);

>该函数与bind用法相同，但只触发一次，随后就要立即解除绑定

##### 模拟操作

> - trigger("click");
> - trigger("myClick");
> - 传递数据
>
>```
>$(".btn").bind("myClick", function(event, msg1, msg2){
> //...
>});
>$().trigger("myClick", ["我的自定义"， "事件"]);
>//
>```
> - 执行默认操作
>
>```
>//不仅会触发focus还会触发浏览器默认操作
>$("input").trigger("focus");
>//不会触发浏览器默认操作
>$("input").triggerHandler("focus");
>```

##### 其他用法

- 绑定多个事件
```
$("div").bind("mouseover mouseout", function(){});
```

- 添加事件命名空间，便于管理
```
$().bind("click", function(){});
$().bind("click.aaa", function(){});
//移除click.aaa
$().unbind(".aaa");
//移除click不含命名空间的事件
$().unbind("click!");
```
