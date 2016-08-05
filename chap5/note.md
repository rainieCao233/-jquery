#### jQuery对表单表格的应用

##### 表单应用

> 一个表单有3个基本组成部分：
> - 表单标签：包含处理表单数据所用的服务器端程序URL以及数据提交到服务器的方法
> - 表单域：包含文本框、密码框、隐藏域、多行文本域、复选框、单选框、下拉选框和文件上传etc
> - 表单按钮：包含提交按钮、复位按钮和一般按钮，用于将数据传送到服务器上或者取消传送，还可以用来控制其它定义了处理脚本的处理。

 - 单行文本框的应用

```
<form action="#" method="post" id="regform">
	<fieldset>
		<legend>个人信息</legend>
		<div>
			<label for="username">username</label>
			<input type="text" id="username">
		</div>
		<div>
			<label for="pass">password</label>
			<input type="pass" id="password">
		</div>
		<div>
			<label for="msg">message</label>
			<textarea id="msg"></textarea>
		</div>
	</fieldset>
</form>
//IE6不支持除了超链接之外元素的:hover
```

- 多行文本框的应用

 - 高度变化
```
<form action="#">
<div class="msg">
		<div class="msg_cap">
			<span class="bigger">放大</span>
			<span class="smaller">缩小</span>
		</div>
		<textarea name="" id="comment" cols="20" rows="8">
			多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框多行文本框
		</textarea>
</div>
</form>
```
```
	$(function(){
		var $comment = $("#comment");
		$(".bigger").click(function(){
			if(!$comment.is(":animated")){
				if($comment.height() < 500){
					// $comment.height( $comment.height() + 50 );
					$comment.animate({ height : "+=50" }, 400);
				}				
			}
		});
		$(".smaller").click(function(){
			//与上函数相反
		});
	});
```
 - 滚动条高度变化
```
	$(function(){
		var $comment = $("#comment");
		$(".up").click(function(){
			if(!$comment.is(":animated")){
				$comment.animate({ scrollTop: "+=50" }, 400);		
			}
		});
		$(".down").click(function(){
			//与上函数相反
		});
	});
```

- 复选框的应用
```
<form action="#">
	Your hobby is...<br />
	<input type="checkbox" name="items" value="足球" />足球
	<input type="checkbox" name="items" value="篮球" />篮球
	<input type="checkbox" name="items" value="羽毛球" />羽毛球
	<input type="checkbox" name="items" value="乒乓球" />乒乓球
	<input type="button" id="checkedAll" value="全 选" />
	<input type="button" id="checkedNo" value="全不选" />
	<input type="button" id="checkedRev" value="反 选" />
	<input type="button" id="send" value="提 交" />
</form>
```
```
$(function(){
	$("#checkedAll").click(function(){
		$("[name=items]:checkbox").attr("checked", true);
	});

	$("#checkedNo").click(function(){
		$("[name=items]:checkbox").attr("checked", false);
	});

	$("#checkedRev").click(function(){
		$("[name=items]:checkbox").each(function(){
			this.checked = !this.checked;
		});
	});

	$("#send").click(function(){
		var str = "你选中的是：/r/n";
		$("[name=items]:checkbox:checked").each(function(){
			str += $(this).val() + "/r/n";
		});
	});
});
```
```
//使用checkbox作为全选/全不选按钮
$("#checkedAll").click(function(){
	$("[name=items]:checkbox").attr("checked", this.checked);
});
$("[name=items]:checkbox").click(function(){
	var $tmp = $("[name=items]:checkbox");
	//使用filter()方法筛选出选中的复选框，并直接给checkedAll赋值
	$("#checkedAll").attr("checked", $tmp.length==$tmp.filter(":checked".length));
});
```
>在有些浏览器中，只要写disabled就可以，有的则需要写disabled = "disabled"; 所以从1.6开始，jquery提供一种prop()方法，返回值为标准属性true/false， eg. $("#checkbox").prop("disabled");
>
>只添加属性名称机会生效的属性应使用prop() eg.checked/disabled
>
>只存在true/false的属性应使用prop()

- 下拉框应用
```
<div class="centent">
	<select multiple name="" id="select1" style="width:100px;height:160px;">
		<option value="1">1</option>
		...
		<option value="8">8</option>
	</select>
	<div>
		<span id="add">添加到右边&gt;&gt;</span>
		<span id="add_all">全部添加到右边&gt;&gt;</span>
	</div>
</div>
<div class="centent">
	<select multiple name="" id="select2" style="width:100px;height:160px;">
	</select>
	<div>
		<span id="remove">&lt;&lt;删除到左边</span>
		<span id="remove_all">&lt;&lt;全部删除到左边</span>
	</div>
</div>
```
```
$(function(){
	$("#add").click(function(){
		var $options = $("#select1 option:selected");

		var $remove = $options.remove();
		$remove.appendTo("#select2");
		//删除和追加可通过appendTo一步完成
		$options.appendTo("#select2");
	});
	$("#add_all").click(function(){
		var $options = $("#select1 option");
		$options.appendTo("#select2");
	});

	$("#select1").dbclick(function(){
		var $options = $("option:selected",this); //$("选择器", 作用域)
		$options.appendTo("#select2");
	});
    //右边添加至左边同上，故不再复述
});
```

- 表单验证
```
//失去焦点函数
$(function(){
	$("form:input").blur(function(){
        var $parent = $(this).parent;
        $parent.find(".formtips").remove(); //删除之前的提示语
        //验证用户名
        if($(this).is("#username")){}
        if($(this).is("#email")){
        	if(this.value=="" || (this.value!="" && !/.+@.+\.[a-zA-Z]{2,4}$/.test(this.value))){
        		//错误提示
        	}else{}
        }	
	});

	$("#send").click(function(){
		$("form:input").trigger('blur');
		var numError = $("form .onError").length;
		if(numError){
			return false;
		}
		alert("success!");
	});

	//输入时即提醒
	$("form:input").blur(function(){
		//失去焦点处理函数...
	}).keyup(function(){
		//trigger('blur')不仅能触发为元素绑定的blur事件还能触发浏览器默认事件，即失去焦点。而triggerHandler("blur")只触发为元素绑定的事件
		$(this).triggerHandler("blur");
	}).focus(function(){
		$(this).triggerHandler("blur");
	});
});
```

##### 表格应用

- 表格变色
```
<table>
	<thead>
		<tr><th>name</th><th>sex</th><th>loc</th></tr>
	</thead>
	<tbody>
		<tr><td>helen</td><td>F</td><td>ningbo</td></tr>
		<tr><td>jack</td><td>M</td><td>hangzhou</td></tr>
		<tr><td>alice</td><td>F</td><td>changsha</td></tr>
		<tr><td>bob</td><td>M</td><td>wenzhou</td></tr>
		<tr><td>rain</td><td>M</td><td>hangzhou</td></tr>
		<tr><td>jenny</td><td>F</td><td>hangzhou</td></tr>
	</tbody>
</table>
```
```
//隔行变色
.even{background:red;}
.odd{background:yellow;}
$("tbody>tr:odd").addClass("odd"); //$("tr:odd")索引从0开始，故第一行是偶数
//设置某一行
$("tbody>tr:contains('jack')").addClass("");
//单选框控制表格行高亮
$("tbody>tr").click(function(){
    $(this).addClass("selected")
           .siblings().remove("selected")
           .end()  //当进行siblings操作时this发生变化，需使用end返回上一层对象
           .find(":radio").attr("checked", true);
});
//含有选中单选框的这一行将被高亮显示
$("tbody>tr:has(:checked)").addClass("selected");
//复选框控制表格高亮
$("tbody>tr").click(function(){
    var hasSelected = $(this).hasClass("selected");
    $(this)[hasSelected?"removeClass":"addClass"]("selected");  //三元运算符控制函数选择
          .find(":checked").attr("checked", !hasSelected);
});
```

- 表格展开关闭
```
<table>
	<thead>
		<tr><th>name</th><th>sex</th><th>loc</th></tr>
	</thead>
	<tbody>
		<tr class="parent" id="row_01"><th colspan="3">设计组</th></tr>
		<tr class="child_row_01"><td>helen</td><td>F</td><td>ningbo</td></tr>
		<tr class="child_row_01"><td>jack</td><td>M</td><td>hangzhou</td></tr>

		<tr class="parent" id="row_02"><th colspan="3">开发组</th></tr>
		<tr class="child_row_02"><td>alice</td><td>F</td><td>changsha</td></tr>
		<tr class="child_row_02"><td>bob</td><td>M</td><td>wenzhou</td></tr>

		<tr class="parent" id="row_03"><th colspan="3">测试组</th></tr>
		<tr class="child_row_03"><td>rain</td><td>M</td><td>hangzhou</td></tr>
		<tr class="child_row_03"><td>jenny</td><td>F</td><td>hangzhou</td></tr>
	</tbody>
</table>
```
```
$("re.parent").click(function(){                        //获取所谓的父行
    $(this).toggleClass("selected")         
           .siblings(".child_"+this.id).toggle();
}).click();                                             //若不加，则默认展开，添加后，默认收缩
```


- 表格内容筛选
```
//根据用户输入来筛选
$("#filterName").keyup(function(){
    $("table tbody tr").hide()
                       .filter(":contains('"+( $(this).val() )+"')").show();
}).keyup();  //不添加时，页面刷新筛选后失效，故需要立即触发该事件
```


##### 其他应用

- 网页字体大小
- 网页选项卡
- 网页换肤



















