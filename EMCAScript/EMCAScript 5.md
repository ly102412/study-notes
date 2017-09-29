# EMCAScript 5
### 严格模式
- 理解
	- 除了正常运行模式(混杂模式)，ES5 添加了第二种运行模式：严格模式（strict mode）
	- 顾名思义，这种模式使的 JavaScript 在更加严格的语法条件下运行
- 目的/作用
	- 消除 JavaScript 语法的一些不合理、不严谨之处，减少一些怪异的行为
	- 消除代码运行的一些不安全之处，为代码的安全运行保驾护航
	- 为未来新版本的 JavaScript 做好铺垫
- 使用
	- 将全局或函数的第一条语句定义为：“use strict”
	- 如果浏览器不支持，只解析为一条简单的语句，没有任何副作用
- 语法限制
	- 必须使用 var 声明变量
	- 禁止自定义的函数中的 this 指向 window
	- 新增 eval 作用域，不能再修改全局中的变量，更安全
		- eval() 解析里面的字符串，并运行里面的字符串代码
	- 对象不能有重名的属性

### JSON 对象
- 作用 -- 用于在 JSON 对象/数组与 JS 对象/数组中相互转换
- JSON.stringify(obj/arr)
	- JS 对象/数组转换为 JSON 对象/数组
- JSON.parse(json)
	- JSON 对象/数组转换为 JS 对象/数组

### Object 扩展
- Object.create(prototype,[descriptors])
	- 作用 -- 以指定对象为原型创建新的对象
	- 参数 
		- prototype -- 对象
			- 老对象的原型属性可以被新创建的对象访问
			- 新创建的对象的隐式原型属性指向第一个参数里对象的显示原型属性
		- descriptors -- 为新的对象指定新的属性并对属性进行描述（以对象的形式）
			- value -- 通过 value 指定值
			- writable -- 标识当前属性值是否是可以修改的，默认值为 true 可以修改
	- 实例代码
		```
			var obj = {
	    		name:'wukong',
	    		age:39
	  		};
	  		var obj1 = {};
	  
	  		obj1 = Object.create(obj,{ //obj是obj1的原型对象
	    		sex:{
	      			value:'男',
	      			writable:true //可修改属性
	    		}
	  		});
	
	  		obj1.sex = "女";
	  		console.log(obj1.sex); //女
		```
- Object.defineProperties(object,descriptors)
	- 作用 -- 为指定对象扩展多个属性
	- 参数
		- object -- 要扩展属性的对象
		- descriptors -- 为对象指定新的属性（对象），使用存取器属性
			- get -- 用来得到当前属性值的回调函数（通过 get 设置的不能直接修改属性）
			- set -- 用来监视当前属性值变化的回调函数
	- 实例代码
		```
			var obj = {
	    		firstName:'wukong',
	    		lastName:"sun"
	  		};
	  		Object.defineProperties(obj,{
	      		fullName:{
	        		get:function () {
	        	 		return this.firstName + "-" + this.lastName
	        		},
	        		set:function (data) {
	        			var names = data.split('-');
	        			this.firstName = names[0]
	            		this.lastName = names[1]
	        		}
	      		}
	  		})
	  		console.log(obj.fullName); //wukong-sun

	  		obj.firstName = 'tim';
	  		obj.lastName = 'duncan'
	  		console.log(obj.fullName); //tim-duncan
	
	  		obj2.fullName = "zrc-sss";
	 	 	console.log(obj.fullName); //zrc-sss
		```

- get propertyName(){}
	- 用来得到当前属性值的回调函数

- set propertyName(){}
	- 用来监视当前属性值变化的回调函数

### Array 扩展
- Array.prototype.indexOf(value)
	- 得到数组值在数组中的第一个下标
- Array.prototype.lastIndexOf(value)
	- 得到数组值在数组中的最后一个下标
- Array.prototype.forEach(function(item, index){})
	- 遍历数组
	- 第一个参数 -- 数组元素
	- 第二个参数 -- 数组元素下标
- Array.prototype.map(function(item, index){})
	- 遍历数组
	- 可在遍历数组后对元素进行修改并返回加工后的新的数组
	- 实例代码
		```
			var arr = [1,2,3,4,5,5];
			var arr1 = arr.map(function (item,index) {
		  	  	return item +10
			})
			console.log(arr,arr1); //[10,20,30,40,50,50]
		```
- Array.prototype.filter(function(item, index){})
	- 遍历数组
	- 对数组进行过滤操作，返回符合条件的值
	- 实例代码
		```
			var arr = [1,2,3,4,5,5];
			var arr1 = arr.filter(function (item,index) {
		  	  	return item > 2
			})
			console.log(arr,arr1); //[3,4,5,5]
		```

### Function 扩展 
- Function.prototype.bind(obj)
	- 作用 -- 将函数内的 this 绑定为 obj，并将函数返回
	- 实例代码
		```
			function fun(age) {
        		this.name = 'kobe';
        		this.age = age;
        		console.log('dddddddddddddd');
    		}
    		var obj = {};
    		fun.bind(obj, 12)(); // dddddddddddddd
    		console.log(obj.name, obj.age); // kobe 12
		```
- 注：bind()与call()和apply()的区别
	- 都能指定函数中的 this
	- call() 和 apply() 是立即调用函数
	- bind() 是将函数返回（没有立即调用，需要手动调用）