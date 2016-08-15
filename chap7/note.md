### jQuery插件的使用和写法
> http://plugins.jquery.com/

#### Validation() 表单验证插件

> http://bassistance.de/jquery-plugins/jquery-plugin-validation
> 
> 内置验证规则：拥有必填，数字，E-mail，url和信用卡号码等19类内置验证规则
> 
> 自定义验证规则：可以很方便的自定义验证规则
> 
> 简单强大的验证信息提示：默认了验证信息提示，并提供自定义覆盖默认提示信息功能
> 
> 实时验证：可以通过keyup或blur事件触发验证，而不仅仅在表单提交的时候验证

```
$(function(){
  $("#form").validate();
});
//针对不同的字段，进行验证规则编码，如下required/url/email/minlength
<label for="cusername">姓名</label>
<input type="" name="username" id="cusername" class="required" size="25" minlength="2" />
<label for="cemail">email</label>
<input type="" name="email" id="cemail" class="required email" size="25" />
<label for="curl">curl</label>
<input type="" name="url" id="curl" class="url" size="25" value="" />
//上例中，将属性写在class中或当作标签属性，不方便管理，故引入jquery.metadata.js
```
- jquery.metadata.js
> jquery.metadata.js是一个支持固定格式解析的jquery插件
> http://plugins.jquery.com/project/metadata

 ```
$("#form").validate({meta:"validate"});
<label for="cusername">姓名</label>
<input type="" name="username" id="cusername" size="25"class="{validate:{required:true, minlength:2}}" />
<label for="cemail">email</label>
<input type="" name="email" id="cemail" size="25" class="{validate:{required:true, email:true}}"  />
<label for="curl">curl</label>
<input type="" name="url" id="curl" size="25" value="" class="{validate:{required:true}}" />
//也可将实现行为与结构分离，每个字段的name值匹配校验规则
$(function(){
	rules:{
		username:{
			required:true,
			minlength:2
		},
		email:{
			required:true,
			email:true
		},
		url:"url"
	}
});
 ```
- 验证信息
 - 国际化
 > Validation验证信息默认英语，若使用中文，则引入validation提供的中文验证信息库
 >jquery.validate.message_cn.js

 - 自定义验证信息
 ```
$(function(){
    $("#form").validate(function(){
	rules:{
		username:{
			required:"请输入姓名",
			minlength:"请输入至少两个字符"
		},
		email:{
			required:"请输入姓名",
			email:"请检查email的格式"
		},
		url:"请检查网址的格式"
	}
    });
});
 ```

 - 自定义验证信息并美化
 ```
    $("#form").validate(function(){
	rules:{
		username:{
			required:"请输入姓名",
			minlength:"请输入至少两个字符"
		},
		email:{
			required:"请输入姓名",
			email:"请检查email的格式"
		},
		url:"请检查网址的格式"
	},
        errorElement:"em",
        success:function(label){
            label.text("").addClass("success");
        }
    });
```

- 自定义验证规则
  ```
    $.validate.addMethod(){
        "formula",
        function(value, element, param){
            return value == eval(param);
        },
        "请输入数学公式计算后的结果"
    }
  ```
  ```
    $("#form").validate(function(){
	rules:{
		username:{
			required:"请输入姓名",
			minlength:"请输入至少两个字符"
		},
		email:{
			required:"请输入姓名",
			email:"请检查email的格式"
		},
		url:"请检查网址的格式",
        valcode:{formula: "7+9"}
	}
    });
  ```

- API
 > 官方API文档：http://docs.jquery.com/Plugins/Validation

#### Form 表单插件

> jQuery Form插件是一个优秀的Ajax插件，可以容易的无侵入的升级HTML表单以支持Ajax。
> 
> 下载地址：http://jquery.malsup.com/form/#download

```
<form action="demo.php" method="post" id="myForm">
	name: <input type="text" name="name" /> <br />
	adderss: <input type="text" name="adderss" /><br />
	selfintro: <textarea name="comment" id="" cols="30" rows="10"></textarea>
	<input type="submit" id="test" value="submit" /><br />
	<div id="output1" style="display:none;"></div>
</form>
```
```
<script src="./jquery.min.js"></script>
<script src="./jquery.form.js"></script>
<script>
$(function(){
	$("#myForm").ajaxForm(function(){
		$("#output1").html("success!").show();
	});
});
</script>
```

- ajaxForm()与ajaxSubmit() 核心方法
 > 以上两函数均可接受1个或者0个参数，当为单个参数时，可为一个回电函数一个options对象。

 ```
 $(function(){
	var options = {
		target: "#output1",         //将服务器返回的内容放入ID为output1的元素中
		beforeSubmit: showRequest,  //提交前的回调函数可进行validate
		success: showResponse,      //提交后的回调函数
		url: url,                   //form的action
		type: type,                 //form的method
		datatype: null,             //xml/json/script接收服务器端返回类型
		clearForm: true,            //成功提交后，清除所有表单元素的值
		resetForm: true,            //成功提交后，重置所有表单元素的值
		timwout: 3000               //限制请求的时间
	}
	$("#myForm").submit(function(){
		$(this).ajaxForm(options);
		return false;
	});
	function showRequest(formData, jqForm, options){
		var queryString = $.param(formData);
		return true;
	}
	function showResponse(responseText, statusText, xhr, $form){
		alert('statusText:' + statusText + '\n responseText:' + responseText);
	}
});
 ```

- 表单提交前验证表单
```
	function validate(formData, jqForm, options){
		// form validate 如果验证不通过return false;
		var queryString = $.param(formData);
		return false;
	}
```

 - 利用参数formData
 > formData是一个数组对象，格式如下，可遍历数组进行验证
 > 
 > [{name:name,value:nameValue},{name:password, value:passwordValue}]

 - 利用jqForm
 > jqForm是一个jQuery对象，它封装了表单的元素
 > 
 > 通过jqForm[0].address.value获取地址的值

 - 利用fieldValue()方法
 > 该方法会把匹配元素的值插入到数组中，然后返回整个数组，若元素的值被判定无效则会返回空
 > 
 > $("input[name=address]").fieldValue();

#### SimpleModal 模态窗口插件

> http://www.ericmmartin.com/projects/simplemodal
> 
> 和bootstrap差不多，爸爸开心了再写


#### Cookie 管理Cookie插件

> 爸爸开心了再写
> 
> 
> 

#### JqueryUI

> 爸爸开心了再写
> 
> 
> 

#### 编写Jquery插件

>
>
>
>

