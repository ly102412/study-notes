# jQuery 类数组操作
- 类数组对象就是结构上类似于数组的对象，该对象具备数组的一些特性属性或方法，同时具有自己独特的一些属性或方法
- 数组与类数组对象的区别
	- 数组的类型是 Array
	- 类数组对象的类型是 Object
- 类数组的操作
	- 属性
		-  length -- 表示长度，指的是当前存储元素的个数
	- 方法
		- 循环遍历方法
			```
				$（）.each（function（index，domEle）{}）
					index -- 遍历过程中的索引值
					domEle -- 遍历后得到的 DOM 对象
				$.each（object，function（index，domEle）{}）
					object -- 需要遍历的对象或数组
					index -- 遍历过程中的索引值
					domEle -- 遍历后得到的 DOM 对象
			```
		- toArray（）方法
	        - 将 jQuery 对象转换成真正的数组
            - 注：只能操作 jQuery 对象
        - $.inArray（value，array）
	        - 作用 -- 判断指定的值在指定数组中的位置（索引值）
			- 注：如果数组包含指定的值 -- 返回对应的索引值;如果数组不包含指定的值 -- 返回固定值 -1
		- $.makeArray（obj）
			- 作用 -- 将类数组对象转换为数组对象