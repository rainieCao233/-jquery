#### Document Object Model

- DOM core
>getElementById() \ getElementByTagName() \ getAttribute() \ setAttribute()...

- HTML-DOM
>document.forms \ element.src

- CSS-DOM
>获取与设置style对象的各种属性
>
>element.style.color =  "red";

#### JQuery DOM

- 查找节点/节点属性
>$("ul li:eq(0)")
>
>$("div").attr("id")

- 创建节点/文本节点/属性节点
>$(html)

- 插入节点

func | example | description
---|---|---
append() | $("div").append(html); | 向div内部追加html
appendTo() | $(html).appendTo("div"); | 向div内部追加html
prepend() | $("div").prepend(html); | 在div内部前置html
prependTo() | $(html).prependTo("div"); | 在div内部前置html
after() | $("div").after(html); | 在div后面添加html
insertAfter() | $(html).insertAfter("div"); | 在div后面添加html
before() | $("div").before(html); | 在div前面添加html
insertBefore() | $(html).insertBefore("div"); | 在div前面添加html

- 删除节点

func | example | description
---|---|---
remove() | $("div").remove(); | 删除div及其后代节点，并返回删除节点的指针
detach() | $("div").detach(); | 用法同上，但此方法下会保留原绑定在删除元素上的事件
empty() | $("div").empty(); | 清空div后代节点

>appendTo()可以用来移动元素
>
>$("ul li:eq(0)").appendTo("ul");

- 复制元素
>$("div").clone(true).appentTo("ul");
>
>clone内参数表示是否复制原绑定在div上的事件

- 替换节点
>$("p").replaceWith(html); 
>
>$(html).replaceAll("p");
>
>以上两种方式均需要重新绑定事件

- 包裹节点
>$("strong").wrap(标签); 使用标签将每一个strong分别包裹起来
>
>$("strong").wrapAll(标签); 将所有strong用一个标签包裹
>
>$("strong").wrapInner(标签); 用标签包裹strong的后代元素

- 属性操作
>获取：$("p").attr("title");
>
>赋值：$("p").attr("title", "hahahahah"); / $("p").attr({"title":"hahahahah", "":"",...});
>
>删除：$("p").removeAttr("title");

- 样式操作
> 获取：$("p").attr("class");
>
> 赋值：$("p").attr("class", "high");
>
> 追加：$("p").addClass("another");
>
> 移除：$("p").removeClass("another");
>
> 切换：$("p").toggleClass("another"); / $btn.toggle(function(){},function(){});
>
> 判断是否使用某个类：$("p").hasClass("another");

- 获取/设置html、文本与值
> - html()
>
>$("div").html();
>
>$("div").html(html);
>
> - text()
>
>$("div").text();
>
>$("div").text(text);
>
> - val()
>
>$("div").val();
>
>$("div").val(val); / $("checkbox").(["checke2", "checke4"]);
>

- 遍历节点
>children()：查找元素的子节点，不包含其余后代节点
>
>next()：获取匹配元素后面紧邻的同辈元素
>
>prev()： 获取匹配元素前面紧邻的同辈元素
>
>siblings()： 获取匹配元素前后所有的同辈元素
>
>closest()： 获取离得最近的匹配元素

func | example | description
---|---|---
parent() | $("").parent() | 获取父元素
parents() | $("").parents("") | 获取所有匹配的祖先元素
closest() | $("").closest() | 获取第一个匹配的祖先元素

- CSS DOM
>$("p").css(""); / $("p").css("", ""); / $("p").css({"":"", "":"",...});
>
>$().height()：获取实际高度，而$().css("height")与样式设置有关，可能会得到auto

func | example | description
---|---|---
offset() | $("").offset().left | 获取元素相对于视窗的偏移
position() | $("").position().left | 获取元素相对于最近的一个被设置绝对/相对定位的元素的偏移
scrollTop() | $("").scrollTop() | 获取滚动距离
scrollLeft() | $("").scrollLeft() | 获取滚动距离
