# jQuery 动画
### 显示和隐藏效果
- 通过同时改变元素的宽度和高度来实现显示或者隐藏
	- 无动画效果
		- 显示 -- show()
		- 隐藏 -- hide()
		- 实例代码
			```
				$("#panel h5.head").click(function(){
				    var $content = $(this).next("div.content");
				    if($content.is(":visible")){
				       $content.hide();
				    }else{
				       $content.show();
				    }
				})
			``` 
	- 有动画效果
		- 显示 -- show(speed,callback)
			- speed -- 预定义三种速度“slow”、“normal”和“fast”，或者自定义时间，单位为毫秒
			- callback -- 动画执行完毕后的回调函数
		- 隐藏 -- hide(speed,callback)
			- speed -- 预定义三种速度“slow”、“normal”和“fast”，或者自定义时间，单位为毫秒
			- callback -- 动画执行完毕后的回调函数
		- 实例代码
			```
				$("#panel h5.head").click(function(){
				    var $content = $(this).next("div.content");
				    if($content.is(":visible")){
				        $content.hide(600);
				    }else{
				        $content.show(600);
				    }
				})
			```

### 滑动式动画效果
- 通过改变高度来实现显示或者隐藏的效果
- 向上滑动 -- slideUp(speed,callback)
	- speed -- 预定义三种速度"slow"、"normal"和"fast"，或者自定义时间，单位为毫秒
    - callback -- 动画执行完毕后的回调函数
- 向下滑动 -- slideDown(speed,callback)
	- speed -- 预定义三种速度"slow"、"normal"和"fast"，或者自定义时间，单位为毫秒
    - callback -- 动画执行完毕后的回调函数
- 实例代码
	```
		$("#panel h5.head").click(function(){
			var $content = $(this).next("div.content");
			if($content.is(":visible")){
				$content.slideUp(600);
			}else{
				$content.slideDown(600);
			}
		})
	```

### 淡入淡出动画效果
- 通过改变不透明度 opacity 来实现显示或者隐藏
- 淡入效果 -- fadeIn(speed,callback)
	- speed -- 预定义三种速度"slow"、"normal"和"fast"，或者自定义时间，单位为毫秒
    - callback -- 动画执行完毕后的回调函数
- 淡出效果 -- fadeOut(speed,callback)
	- speed -- 预定义三种速度"slow"、"normal"和"fast"，或者自定义时间，单位为毫秒
    - callback -- 动画执行完毕后的回调函数
- 将指定元素的透明度改变到指定值 --  fadeTo（speed，opacity）
- 实例代码
	```
		$("#panel h5.head").click(function(){
			var $content = $(this).next("div.content");
				if($content.is(":visible")){
					$content.fadeOut(600);
			}else{
					$content.fadeIn(600);
			}
		})
	```

### 动画切换效果
- toggle(duration,complete) -- 显示或隐藏匹配元素
	- duration -- 一个字符串或者数字决定动画将运行多久
	- complete -- 在动画完成时执行的回调函数
	- 实例代码
		```
			$('#clickme').click(function() {
			    $('#book').toggle('slow', function() {
			        // Animation complete.
			    });
			});
		```
- slideToggle(duration,complete) -- 用滑动动画显示或隐藏一个匹配元素
	- duration -- 一个字符串或者数字决定动画将运行多久
	- complete -- 在动画完成时执行的回调函数
	- 实例代码
		```
			$('#clickme').click(function() {
			    $('#book').slideToggle('slow', function() {
			        // Animation complete.
			    });
			});
		```

### 自定义动画效果
- animate（params，[ duration ]，[ easing ]，[ callback ]）
	- params -- 表示用于实现动画效果的 CSS 样式属性
	    - 格式 -- Object 类型{ name： value，name：value，……}
    - duration -- 表示动画所执行的时长，预定义三种速度"slow"、"normal"和"fast"，或者自定义时间，单位为毫秒
    - easing -- 要使用的擦除效果的名称（需要插件支持）（可选）
    - callback -- 动画执行完毕后执行的函数（可选）
    - 实例代码
    	```
			$("#panel").click(function(){
			   $(this).animate({left: "500px"}, 3000);
			})
		```
- animate（params，options）
    - params -- 表示用于实现动画效果的 CSS 样式属性
	    - 格式 -- Object 类型{ name： value，name：value，……}
    - options
        - 格式 -- Object 类型
        - 可选项
	        - duration -- 表示动画所执行的时长，预定义三种速度"slow"、"normal"和"fast"，或者自定义时间，单位为毫秒
            - easing -- 要使用的擦除效果的名称（需要插件支持）
            - complet -- 动画执行完毕后执行的函数
            - queue -- 为 true 时为排对效果，为 false 时为并发效果 
	- 实例代码
		```
			$("#panel").click(function(){
				$(this).animate({left: "500px"}, 3000);
			})
		```
> 注意事项
> animate 方法不接受以下属性
> backgroundColor
> borderBottomColor
> borderLeftColor
> borderRightColor
> borderTopColor
> Color
> outlineColor

### 并发与排队效果
- 并发效果 -- 指的就是多个动画效果同时执行
	```
		$("#panel").click(function(){
		   $(this).animate({left: "500px",height:"200px"}, 3000);
		})
	```
- 排队效果 -- 指的就是多个动画按照先后顺序执行
	```
		$("#panel").click(function(){
		    $(this).animate({left: "500px"}, 3000).animate({height: "200px"}, 3000);
		})
	```
			

			
 