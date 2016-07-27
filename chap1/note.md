- ### window.onload与$(document).ready()的对比

> #### window.onload
>
> ##### 执行时机 
>
> 必须等待页面中所有内容加载完毕后才能执行 
>
> ##### 编写个数 
>
> 不能同时编写多个,以下代码无法同时正确执行：
> ```
> window.onload=function(){
>     alert("test1");
> }
> window.onload=function(){
>     alert("test2");
> }
> //结果只会输出text2
> ```
> ##### 简化写法
> 无
>  #### $(document).ready()
>
> ##### 执行时机 
>
>  网页中所有的DOM结构绘制完毕后就执行，可能DOM元素关联的东西并没有加载完
>
> ##### 编写个数 
>
> 能同时编写多个,以下代码同时正确执行：
> ```
> $(document).ready(function(){
>   alert("hello world!")
> });
> $(document).ready(function(){
>   alert("hello again!")
> });
> //结果两次都会输出
> ```
> ##### 简化写法
> ```
> $(document).ready(function(){
> //...
> });
> //可以简写成
> $(function(){
> //...
> });
> ```

- ### DOM对象与JQuery对象的对比

> JQuery对象就是包装DOM对象后产生的对象
>
> JQuery转化为Dom:[index]与get(index)
>
>Dom转JQuery: $()


- ### 解决JQuery与其他库的冲突

> 默认情况下JQuery使用$作为自身的快捷方式
>```
>//将控制权交于其他库
> jQuery.noConflict();
>//继续使用jQuery
>jQuery(function(){
>  jQuery("p").click(function(){});
>});
>```  
>
>```
>//可自定义备用名称
>var $j = jQuery.noConflict();
>$j(function(){
>  $j("p").click(function(){});
>});
>```
> 若不想使用备用名称，可使用以下两种方式可安全使用$()方法：
>```
>jQuery.noConflict();
>jQuery(function($){
>  //使用jQuery设定页面加载时的执行函数
>});
>```
>```
>jQuery.noConflict();
>(function($){
>  //可通过创建闭包，并将jQuery以参数传递进去实现，此时$为形参名称
>})(jQuery);
>```