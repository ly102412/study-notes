# jQuery 基础内容
### jQuery 工厂函数
-  jQuery 的工厂函数算作是 jQuery 的一个入口，通过它既可以使用选择器，也可以包装 DOM 对象，还可以创建元素
-  工厂函数的两种写法
	-  第一种 -- `$()`
	-  第二种 -- `jQuery()`
	-  注 -- 这里的 $ 符号就表示 jQuery ，是 jQuery 的一个约定，而且，jQuery 也建议通过 jQuery 获取的元素变量前都增加 $ 符号

### jQuery 对象与 DOM 对象
- DOM 对象
	- 定义 -- 通过 DOM 获取的元素
- jQuery 对象
    - 定义 -- 通过包装 DOM 对象后产生的一种对象（jQuery 自定义的全局对象）   
    - 注：jQuery 的底层其实还是 DOM 对象，jQuery 是类数组对象，所以 jQuery 对象中可能包含多个 DOM 对象或一个 DOM 对象
- DOM 对象与 jQuery 对象的相互转换
	- DOM 对象转换为 jQuery 对象
	   - 通过 jQuery 的 $( ) 工厂函数将其包裹，返回的就是对应的 jQuery 对象
       - 实例代码
       		```
				// DOM对象
	        	var username = document.getElementById("username");
	        	// DOM对象转换为jQuery对象
	        	var $username = $(username);
			```
	- jQuery 对象转换为 DOM 对象
        - jQuery 对象是类数组对象，可以通过 jQuery 对象[ 索引值 ]直接转换为对应的 DOM 对象
        - 实例代码
        	```
				// jQuery对象
	        	var $user = $("#username");
	        	// jQuery对象是数组对象
	        	var user1 = $user[0];
			```

		- jQuery 提供了get（index）方法，通过 jQuery 对象.get（索引值）方法进行转换
		- 实例代码
			```
				// jQuery对象
	        	var $user = $("#username");
	        	// jQuery提供get(index)方法进行转换
	        	var user2 = $user.get(0);
			```
- 注：在实际开发中，DOM 和 jQuery 可以混合使用