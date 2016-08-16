### jQuery性能优化与技巧

#### jQuery性能优化

- 使用最新的JQuery类库
> 建议使用最新版本的JQuery来提高性能，但并不是完全向后兼容的

- 使用合适的选择器
> 尽量使用ID选择器，尽量给元素指定上下文
 - $("#id") 调用getElementById
 - $("p") 调用getElementByTagName
 - $(".class") 调用getElementByClassName
 - $("[attribute=value]") js没有直接实现，性能不佳，需要搜索每一个元素
 - $(":hidden") js没有直接实现，性能不佳，需要搜索每一个元素

- 缓存对象
> 永远不要让相同的选择器在你的代码中出现多次

 ```
$("#xx").css();
$("#xx").fadeIn();
//上面的写法将会在创建美衣一个选择器的过程中查找DOM，创建多个Jquery对象
var $xx = $("#xx");
$xx.css();
$xx.fadeIn();
//当然链式更好
$("#xx").css().fadeIn();
 ```
 ```
//若你打算在其他函数中使用jquery对象，可缓存至全局环境中
window.$my = {
	head : $("head"),
	traffic_light : $("#traffic_light")
}
 ```

- 循环时的DOM循环
```
var top_100_list = [], $mylist = $("#mylist");
for(){
	$mylist.append("...");
}
//以上方法将做100次append操作
var top_100_list = [], $mylist = $("#mylist"), top_100_li = "";
for(){
	top_100_li += "...";
}
$mylist.html(top_100_li);
```

- 数组方式使用jQuery对象
> 建议使用for或者while来处理，而不是$.each()
>
> 检查长度也是检查jQuery对象是否存在的方式

- 事件代理
> 少绑定些事件，如相似节点同样事件可绑定在父节点

 ```
$("parentnode").on("click", "childnode", function(){})
 ```

- 转化为JQuery插件
> 将你的代码转化为JQuery插件，可提高重用性

- 使用join()来拼接字符串

 ```
var top_100_list = [], $mylist = $("#mylist"), top_100_li = [];
for(){
	top_100_li[i] = "...";
}
$mylist.html(top_100_li.join(''));
 ```

- 合理利用H5的data属性

 ```
<div id="dl" data-role="" data-last-value="" data-options='{"name":"john"}'></div>
$("#dl").data("role");
$("#dl").data("lastValue");
$("#dl").data("options").name;
 ```

- 尽量使用原声的JS方法

 ```
$cr.is(":checked")->$cr.get(0).checked;
$(this).css()->this.style.css="";
$("<p></p>")->$(document.createElement("p"));
//方法选择很重要，有时并不需要JQuery ( ˘•灬•˘ )
 ```

- 压缩JS
 - GZIP
 - 去除js文档内注释、空白并压缩局部变量长度等


#### jQuery技巧
> 查看chap11.html
