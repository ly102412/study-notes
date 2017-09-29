# ECMAScript 6
## 常用
### let 关键字
- 作用 -- 用于声明一个变量，与 var 类似
- 特点 
	- 在块作用域内有效
	- 不能重复声明
	- 不会预处理，不存在提升
- 应用
	- 循环遍历加监听
- 实例代码
	```
		<!DOCTYPE html>
		<html lang="en">
		<head>
  			<meta charset="UTF-8">
  			<title>let关键字</title>
		</head>
		<body>
			<button>测试1</button>
			<br>
			<button>测试2</button>
			<br>
			<button>测试3</button>
			<br>

		<script type="text/javascript">
    		let btns = document.getElementsByTagName('button');
    		for(let i = 0;i<btns.length;i++){
            	btns[i].onclick = function () {
                	alert(i);
            	}
    		}

		</script>
		</body>

		</html>
	```

### const 关键字
- 作用 -- 定义常量
- 特点 -- 不可修改
- 应用 -- 保存不需要改变的数据

### 变量的解构与赋值
- 作用 -- 从对象或数组中提取数据，并赋值给（多个）变量
- 对象的解构赋值
	- `let{n,a} = {n:"tom",a:12}` 
- 数组的解构赋值
	- `let[a,b] = [1,"wukong"]`
- 用途 -- 给多个形参赋值
- 实例代码
	```
		let {n, a} = {n:'tom', a:12}
		console.log(n,a) //tom,12

	    let arr = [123,'abc',true];
	    let [a,b,c] = arr; 
	    console.log(a,b,c); //123,'abc',true

	    let obj = {name:'kobe',age:39}
		function person({name,age}) {
		  	 console.log(name,age);
		}
	    person(obj)  //kobe 39
	```

### 模板字符串
- 简化字符串拼接的过程
- 用法
	- 模板字符串必须使用 ``
	- 变化的部分使用 ${} 定义
- 实例代码
	```
		let obj = {name:'kobe',age:39}
		//普通字符串拼串
  		console.log('我叫:' + obj.name + ', 我的年龄是:' + obj.age);
		//模版字符串拼接
	    console.log(`我叫:${obj.name},我的年龄是:${obj.age}`);
	```

### 简化对象的写法
- 省略同名的属性值
- 省略方法的 function
- 实例代码
	```
		//普通写法
		let obj = {
		  x : x,
		  getPoint:function () {
		     return this.x 
		  }
	    }

		//简化写法
		let x = 5
		let obj = {
		   x ,
		   getPoint(){
			 return this.x
		  }
		}
	```

### 箭头函数
- 作用 -- 定义匿名函数
- 基本语法
	- 左侧没有形参并且函数只有一条语句，左侧的 () 不能省略
		- 实例代码
			```
				let fun1 = () =>console.log("fun1()")
				fun1();
			```
	- 左侧有一个形参并且函数只有一条语句，左侧的 () 可以省略也可以不省略
		- 实例代码
			```
				let fun3 = x => console.log(x);
				fun3(45);
				let fun4 = (x) => console.log(x);
				fun4(58);
			```
	- 左侧有两个或两个以上的形参，左侧的 () 不可以省略
		- 实例代码
			```
				let fun2 = (x,y) => console.log(x,y)
				fun2(45,55);
			```
	- 右侧有一个语句或者表达式时，{} 可以省略，省略不写时会自动返回结果；如果没有省略，需要手动返回
		- 实例代码
			```
				let fun5 = (x,y) => x+y;
				console.log(fun5(10,5));
				let fun6 = (x,y) => {return x+y};
				console.log(fun6(5,8));
			```
	- 右侧不止有一个语句或者表达式时，{} 不可以省略，需要手动返回结果
		- 实例代码
			```
				let fun7 = (x,y) => {
					console.log(x,y);
					return x+y;
				};
				console.log(fun7(5,8));
			```
- 箭头函数的特点
	- 简洁
	- 箭头函数没有自己的this，箭头函数的this不是调用的时候决定的，而是在定义的时候处在的对象就是它的this（官方定义）
	- 箭头函数的this看外层的是否有函数，如果有，外层函数的this就是内部箭头函数的this，如果没有，则this是window（自己理解）

### 三点式运算符
- 用途
	- rest（可变）参数
		- 用来取代arguments 但比 arguments 灵活,只能写在形参的最后一位
		- 实例代码
			```
				 fun(...values) {
					console.log(arguments);
        			arguments.forEach(function (item, index) {
            			console.log(item, index);
        			});
        			console.log(values);
        			values.forEach(function (item, index) {
            			console.log(item, index);
        			})
    			}
    			fun(1,2,3);
			```
    - 扩展运算符
	    - 实例代码
	    	```
				let arr1 = [1,3,5];
				let arr2 = [2,...arr1,6];
				arr2.push(...arr1);
			```

### 形参默认值
- 当不传参数的时候默认使用形参里的默认值
- 直接给形参赋值
	- 实例代码
		```
		  function Point(x=0,y=0) {
		    this.x = x;
		    this.y = y;
		  }
		  let p = new Point()
		  console.log(p);  //x=0,y=0
		  let p1 = new Point1(25,36)
		  console.log(p1); //x=25,y=36
		```

### class 类的继承
- 通过class定义类
- 在类中通过constructor定义构造方法
- 通过new来创建类的实例
- 通过extends来实现父类对子类的继承
- 通过super调用父类的构造方法
	- 可重写从父类中继承的一般方法(子类自身重新定义)
- 实例代码
	```
		//class定义类
	  	class Person {
	    	//通过constructor定义构造方法
	    	constructor(name,age){
	      		this.name = name;
	      		this.age = age;
	      		this.showName = function () {
	      	  		return this.name
	      		}
	    	}
	    	showName (){ //定义一般的方法
	      		console.log(this.name);
	    	}
	  	}
	  	let person = new Person('wukong',39);
	  	console.log(person,person.showName()); 
	
	  	//定义一个子类 通过extends来实现父类对子类的继承
	  	class starPerson extends Person{
	    	constructor(name,age,salary){
	      		super(name,age); //super调用父类的构造方法
	      		this.salary = salary;
	    	}
	    	showName(){ //父类的方法重写(在子类自身定义方法)
	      		console.log(this.name,this.age,this.salary);
	    	}
	  	}
	  	let p2 = new starPerson('sun',12,1235453);
	  	console.log(p2); 
	  	p2.showName() 
	```

### Promise 对象
- 概念
	- Promise对象: 代表了未来将要发生的事件(通常是一个异步操作)
  	- 有了promise对象, 可以将异步操作以同步的流程表达出来, 避免了层层嵌套的回调函数(俗称'回调地狱')
  	- ES6的Promise是一个构造函数, 用来生成promise实例
- 基本使用步骤
	- 创建 promise 对象
		- 实例代码
			```
				let promise = new Promise((resolve, reject) => {
					//初始化promise状态为 pending
					//执行异步操作
					if(异步操作成功) {
						resolve(value);//修改promise的状态为fullfilled
					} else {
						reject(errMsg);//修改promise的状态为rejected
      				}
    			})
			```

	- 调用 promise 的 then()
		- 实例代码
			```
				promise.then(function(
					result => console.log(result),
					errorMsg => alert(errorMsg)
				))
			```

- promise 对象的三个状态
	- pending -- 初始化状态
	- fullfilled -- 成功状态
	- rejected -- 失败状态

- 应用
	- 使用 promise 实现超时处理
	- 使用 promise 封装处理 ajax 请求
		- 实例代码
			```
				let request = new XMLHttpRequest();
				request.onreadystatechange = function () {
				}
				request.responseType = 'json';
				request.open("GET", url);
				request.send();
			```
- 实例代码
	```
		//定义一个请求news的方法
		function getNews(url) {
			//创建一个promise对象
			let promise = new Promise((resolve, reject) => {
            	//初始化promise状态为pending
            	//启动异步任务
            	let request = new XMLHttpRequest();
            	request.onreadystatechange = function () {
                	if(request.readyState === 4){
                    	if(request.status === 200){
                        	let news = request.response;
                        	resolve(news);
                    	}else{	
                        	reject('请求失败了。。。');
                    	}
                	}
            	};
            	request.responseType = 'json';//设置返回的数据类型
            	request.open("GET", url);//规定请求的方法，创建链接
            	request.send();//发送
        	})
        	return promise;
    	}

    	getNews('http://localhost:3000/news?id=2')
            	.then((news) => {
	                console.log(news);
	                document.write(JSON.stringify(news));
	                console.log('http://localhost:3000' + news.commentsUrl);
	                return getNews('http://localhost:3000' + news.commentsUrl);
            	}, (error) => {
                	alert(error);
            	})
            	.then((comments) => {
	                console.log(comments);
	                document.write('<br><br><br><br><br>' + JSON.stringify(comments));
            	}, (error) => {
                	alert(error);
            	})
	```

## 其它
### 字符串扩展
- includes(str) -- 判断是否包含指定的字符串
- startsWith(str) -- 判断是否以指定字符串开头
- endsWith(str) -- 判断是否以指定字符串结尾
- repeat(count) -- 指定重复次数

### 数值的扩展
- 二进制与八进制数值表示法 -- 二进制用0b, 八进制用0o
- Number.isFinite(i) -- 判断是否是有限大的数
- Number.isNaN(i) -- 判断是否是NaN
- Number.isInteger(i) -- 判断是否是整数
- Number.parseInt(str) -- 将字符串转换为对应的数值
	- 忽略字符串中的非数字字符
	- 如果第一个数不是数字则放回 NaN
- Math.trunc(i) -- 直接去除小数部分

### 数组扩展
- Array.from(v) -- 将伪数组对象或可遍历对象转换为真数组
	- 真数组可以使用 forEach() 进行遍历
- Array.of(v1, v2, v3) -- 将一系列值转换成数组
	- 实例代码
		```
			let arr = Array.of(1, 'abc', true);
			console.log(arr); // 输出的是一个数组
		```
- find(function(value, index, arr){return true}) -- 找出第一个满足条件返回true的元素
	- 实例代码
		```
			let arr1 = [1,3,5,2,6,7,3];
				let result = arr1.find(function (item, index) {
					return item >3
				});
    		console.log(result); //5
		```
- findIndex(function(value, index, arr){return true}) -- 找出第一个满足条件返回true的元素下标
	- 实例代码
		```
			let result1 = arr1.findIndex(function (item, index) {
        		return item >3
    		});
    		console.log(result1);//2
		```

### 对象扩展
- Object.is(value1,value2) -- 判断两个数据是否完全相等（判断的是两个数据长得是不是一模一样,与 == 符号不同）
	- 实例代码
		```
			console.log(NaN == NaN);//false
    		console.log(Object.is(NaN, NaN));//true

    		console.log(0 == -0);//true
    		console.log(Object.is(0, -0));//false
		```
- Object.assign(target,source1,source2) -- 将源对象的属性赋值到目标对象上
	- 实例代码
		```
			let obj = {name : 'kobe', age : 39};
    		let obj1 = {};
    		Object.assign(obj1, obj);
    		console.log(obj1, obj1.name);
		```
- 直接操作 __proto__ 属性
	- 实例代码
		```
			let obj3 = {name : 'anverson', age : 41};
    		let obj4 = {};
    		obj4.__proto__ = obj3;
    		console.log(obj4, obj4.name, obj4.age);
		```

### Set() 和 Map() 数据结构
- Set 容器 -- 无序不可重复的多个 value 的集合体
	- 主要功能 -- 数组去重
	- 语法 -- `let set = new Set([1,2,3,4,5,6,5,6,5,5])` 
	- Set 容器的其他方法
		- add(value) 添加值
		- delete(value) 删除值
		- has(value) 判断是否有该值（返回值是布尔值）
		- clear() 清楚
		- size 长度
	- 实例代码
		```
			// 数组去重
			let arr = [1,2,3,4,4,2,1];
			let arr1 = arr;
			arr = [];
			let set = new Set(arr1);
			set.forEach(function(item){
				arr.push(item);
			});
			console.log(arr)
		```
- Map 容器 -- 无序的不重复的多个 key-value 的集合体
	- 该容器仅支持二维数组
	- 前面的值是 key 值，后面的值的 value 值
	- 语法 -- `let map = new Map([['abc',123]])`
	- 输出 -- `Map(1){'abc'=>123}`
	- Map 容器的其他方法
		- set(key，value) 添加 key-value 键值对
		- get(key) 获取 key 对应的 value 值
		- delete(key) 删除值
		- has(key) 判断是否有该值（返回值是布尔值）
		- clear() 清除
		- size 一个二维数组是一个长度

### for_of 遍历循环
- 语法 -- for(let value of target){}
- 参数
	- value 变量
	- target 要循环遍历的目标
- 作用
	- 遍历数组
	- 遍历 Set
	- 遍历 Map
	- 遍历字符串
	- 遍历伪数组