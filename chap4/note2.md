#### jQuery中的动画

##### show()与hide()
 - show()

>不断增加元素height/width/opacity，再将元素display属性值设置为block或者inline

 - hide()

>不断减少元素height/width/opacity，再将元素display属性值设置为none

```
$().show("slow"); //slow->600ms; normal->400ms; fast->200ms
$().show(1000);
```

##### fadeIn()与fadeOut()
 - fadeIn()

>不断增加元素opacity，再将元素display属性值设置为block或者inline

 - fadeOut()

>不断减少元素opacity，再将元素display属性值设置为none

```
$().fadeIn("slow"); //slow->600ms; normal->400ms; fast->200ms
$().fadeIn(1000);
```

##### slideUp()与slideDown()
 - slideUp()

>不断增加元素height，再将元素display属性值设置为block或者inline

 - slideDown()

>不断减少元素height，再将元素display属性值设置为none

```
$().slideUp("slow"); //slow->600ms; normal->400ms; fast->200ms
$().slideUp(1000);
```

##### animate(params, speed, callback);
 - params：一个包含样式属性及值的映射
 - speed：速度参数，可选
 - callback：在动画完成时执行的函数

```
$().animate({left："500px"}, 3000);
$().animate({left："+=500px"}, 3000);
$().animate({left："+=500px", height："200px"}, 3000);
$().animate({left："+=500px"}, 3000).animate({height："200px"}, 3000);
```

##### 动画回调函数

```
$().animate({left："+=500px"}, 3000, function(){
    //...
});
```
##### 停止动画与判断
 - stop([clearQueue], [gotoEnd]);
>clearQueue：是否要清空未完成的动画队列
>gotoEnd：是否直接将正在执行的动画跳转到末状态

```
$().hover(function(){
    $().stop().animate({height:"30px"}, 200)
                  .animate({left:"30px"}, 200);
}, function(){
    $().stop().animate({height:"30px"}, 200)
                  .animate({left:"30px"}, 200);
});
//stop不带参数状态下，当光标在height改变时移出元素，只会终止当前正在进行的动画，然后继续进行left动画，此时，stop的第一个param就发挥作用了，它会清空所有动画队列
//gotoEnd仅能设置正在执行的动画的最终状态，而不能直接到达未执行动画队列的最终状态
```

 - 判断是否处于动画状态

```
$().is(":animated")
```
 - 延迟动画

```
$().delay(1000).animate();
```

##### 其他动画
 - toggle()

>切换元素可见状态

 - slideToggle()

> 切换slideUp()与slideDown()

 - fadeTo()

```
$().fadeTo(600, 0.2);
```

 - fadeToggle()

>切换fadeIn()与fadeOut()

##### 动画方法概括