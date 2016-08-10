### JQuery与Ajax的应用
> Ajax 全称为 Asynchronous Javascript XML，他并不是一种单一的技术，而是有机的利用了一系列交互式网页应用相关的技术所形成的结合体。

#### Ajax的优势与不足

- 优势
 - 不需要插件支持
 - 优秀的用户体验
 - 提高web程序的性能
 - 减轻服务器端和带宽的压力

- 不足
 - 浏览器对XMLHttpRequest对象的支持度不足
 - 破坏浏览器前进、“后退”按钮的正常功能
 - 对搜索引擎的支持不足
 - 开发和调试工具的匮乏

#### XMLHttpRequest对象
> Ajax的核心是XMLHttpRequest，XMLHttpRequest对象提供了一个相对于简易的API方便程序员的开发。

- 属性
 - readystate属性
 > readystate标识了当前XMLHttpRequest正处于什么状态，由此来判断应作出什么样的操作。
 
值 | 说明
:---:|:---
0 | 未初始化状态，此时已经创建了一个XMLHttpRequest对象，但还是没有开始初始化
1 | 准备发送状态：此时已经调用了XMLHttpRequest对象的open()方法，且XMLHttpRequest已经做好准备发送至服务端
2 | 已发送状态：此时已经通过send()方法把一个请求发送到服务器端，但是还没有收到一个响应
3 | 正在接受状态：此时已经接收到了HTTP响应头不信息，但是消息体部分还没有完全接收到
4 | 完成响应状态：此时已经完成了HttpResponse响应的接收

 - responseText属性
 > responseText属性包含客户端接收到的HTTP响应的文本内容

readystate值 | responseText值
:---:|:---
0/1/2 | 空字符串
3 | 客户端还未完成的响应信息
4 | 包含完整的响应信息

 - responseXML属性
 > 当readystate==4并且响应头部Content-Type的MIME类型被指定为XML时，该属性才会有值并且被解析为一个XML文档，否则该属性值为null

 - status属性
 > status属性描述了HTTP状态代码，仅当readystate值为3或4时，才能对此属性进行访问，否则会报异常

 - statusText属性
 > statusText属性描述了HTTP状态代码文本

- 事件
 - onreadystatechange事件
 > 当readystate状态码发生改变时会调用此函数

 - open(method, uri, async, username, password)方法
 > 使用该方法将会得到一个send()方法的对象
 >
 > method:必选，用于指定发送请求的HTTP方法，参数要大写
 >
 > uri:用于指定XMLHttpRequest对象把请求发送到服务器
 >
 > async:用于标识请求是否是异步的，默认值为true
 >
 > username/password:服务器上的身份标识

 - send()
 > 调用open()后且readystate==1时可以调用send()方法将请求进行发送

 - abort()
 > 暂停请求的发送或接受，并将XMLHttpRequest对象设置为初始化状态

 - setRequestHeader()
 > 当readystate==1且调用open()后可用来设置请求头信息

 - getRequestHeader()
 > 当readystate==3/4可用来获取请求头信息，否则返回空字符串

#### Ajax的应用

- 安装

- 第一个Ajax例子

- jQuery中的Ajax
 - load("filename selector", function(responseText, textStatus, XMLHttpRequest){});
 - $.get(url, [data], function(data, textStatus){}, [type]);
 - $.post();使用方法同上
 - $.getScript(".js", function(){}); 动态添加js
 - $.getJSON(".js", function(){});
 - $.each(data, function(index, ele){});
 - $.ajax(options);
 > options:url\type\timeout\data\dataType\beforeSend\complete\success\error\global

- 序列化元素
 - serialize()方法
 > 将DOM元素内容序列化为字符串

 ```
 $.get("get.php", $("#form1").serialize(), function(data, textStatus){});
 ```

 - serializeArray()方法
 > 将DOM元素序列化后返回JSON格式的数据

 - $.param()
 > 对一个数组或对象按照key/value进行序列化

#### Ajax中的全局事件

方法名称 | 说明
---|---
ajaxStart() | 请求开始时
ajaxStop() | 请求结束时
ajaxComplete() | 请求完成时
ajaxError() | 请求发生错误时
ajaxSend() | 请求发送前
ajaxSuccess() | 请求成功