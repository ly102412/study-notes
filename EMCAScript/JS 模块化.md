# JS 模块化
### 简介
- 将一个复杂的程序依据一定的规则（规范）封装成几个块（文件），之后将其组合在一起
- 块内部的数据实际是私有的，只是向外暴露一些接口（方法）与外部其他模块通信

### 模块化的好处（理想）
- 避免命名冲突（减少命名空间污染）
- 更好的分离，按需加载
- 更高的复用性
- 更高的可维护性(每个模块)

### 模块化的问题（实际）
- 请求过多
- 依赖模糊
- 难以维护（主体模块）

### 模块化的演变历史
#### 全局函数模式 -- 将不同的功能封装成不同的全局函数
- 问题 -- 全局被污染，很容易引起命名冲突，数据可以在外部被直接修改
- 实例代码
	```
	module1.js
		let msg = "llc";
		function foo(){
			console.log("module1 foo");
		};
		function bar(){
			console.log("module1 bar");
		};
	```
	```
	module2.js
		let xin = "qhf";
		function foo(){
			console.log("module2 foo"); // 与另一个函数重名了
		};
	```
	```
	<script type="text/javascript" src="module1.js"></script>
	<script type="text/javascript" src="module2.js"></script>
	<script type="text/javascript">
		foo(); // module2 foo(被重名函数替换)
		bar(); // module1 bar
	</script>		
	```

#### namespace 模式 -- 简单对象封装
- 作用 -- 减少了全局变量
- 问题 -- 不安全（数据不是私有的，外部可以修改）
- 实例代码
	```
	module1.js
		let myModule = {
			username:"llc",
			foo(){
				console.log(this.username)
			}
		};
	```
	
	```
	module2.js
		let myModule1 = {
			username:"qhf",
			foo(){
				console.log(this.name)
			}
		};
	```

	```
	<script type="text/javascript" src="module1.js"></script>
	<script type="text/javascript" src="module2.js"></script>
	<script type="text/javascript">
		myModule.foo();	// llc
		myModule1.foo(); // qhf
		myModule.username = "jyl"; //修改 myModule 中的 username
		myModule.foo(); // jyl
	</script>
	```

#### IIFE 模式 -- 匿名函数自调用（闭包）
- IIFE -- immediately-invoked function expression(立即调用函数表达式) 
- 作用 -- 数据是私有的，外部只能通过暴露的方法操作
- 问题 -- 有可能当前的模块依赖另一个模块
- 实例代码
	```
	module1.js
		(function (widow){
			let msg = "llc";
			let msg1 = "qhf";
			function foo(){
				console.log("llc");
			};
			function bar(){
				console.log("qhf");
			};
			window.myModule = {foo,bar};
		})(window);
	```

	```
		<script type="text/javascript" src="module.js"></script>
		<script type="text/javascript">
  			myModule.foo(); // llc
  			myModule.bar(); // qhf
  			myModule.mag = 'jyl' //不是修改的模块内部的data
  			myModule.foo() //llc
		</script>
	```

#### IIFE 模式增强 
- 引入依赖
- 是现代的模块化实现的基石
- 实例代码
	```
	module1.js
		(function (widow,$){
			let msg = "llc";
			let msg1 = "qhf";
			function foo(){
				console.log("llc");
				$("body").css("background","red");
			};
			function bar(){
				console.log("qhf");
			};
			window.myModule = {foo,bar};
		})(window,jQuery);
	```

	```
		<script type="text/javascript" src="jquery-1.10.1.js"></script>
		<script type="text/javascript" src="module.js"></script>
		<script type="text/javascript">
  			myModule.foo(); 
		</script>
	```

#### 页面加载多个 JS
- 一个页面经常需要引入多个 JS
- 问题
	- 请求过多
	- 依赖模糊
	- 难以维护
- 这些问题可以通过现代模块化编码

### 模块化规范
#### CommonJs
- 说明
	- 每一个文件都可以作为一个模块
	- 在服务器端 -- 模块的加载是运行时同步加载的
	- 在浏览器端 -- 模块需要提前编译打包处理
- 基本语法
	- 暴露模块
		- module.exports = value（暴露的是 exports 对象）
		- exports.xxx = value（暴露的是 exports 对象的一个属性）
	- 引入模块
		- require（模块名）-- 第三方或自带模块
		- require（文件相对路径）-- 自定义模块
- 实现
	- 服务器端 -- Node.js
	- 浏览器端 -- browserify（打包工具）
- 区别
	- Node.js 运行时动态加载模块（同步）
	- Browserify 是在转译（编译）时就会加载打包（合并）require 的模块

##### Node.js 模块化
- 下载 node.js
- 构建项目
	```
		|-modules // 模块文件
  			|-module1.js
  			|-module2.js
  			|-module3.js
		|-app.js // 主文件
		|-package.json
  			{
    			"name": "commonJS-node",
    			"version": "1.0.0"
			} 
	```
	- （注：第三方模块 -- uniq -- 对数组进行去重并且重新排序）
- 模块化编码
	- module1.js
		```
			module.exports = {
				foo(){
					console.log("module1");
				};
			};
		```
	- module2.js
		```
			module.exports = function () {
				console.log("module2");
			};
		```
	- module3.js
		```
			exports.foo = function () {
				console.log("module3 foo");
			};
			exports.bar = function () {
				console.log("module3 bar");
			};
		```
- 主文件引入模块
	```
		let module1 = require("./modules/module1");
		let module2 = require("./modules/module2");
		let module3 = require("./modules/module3");

		module1.foo(); // module1
		module2();  // module2
		module3.foo(); // module3 foo
		module3.bar(); // module3 bar 
	```
- 通过 node 运行 app.js
	- 命令 -- node app.js
	- 工具 -- 右键 --> 运行

##### Browserify 模块化
- 构建项目
	```
		|-js
  			|-dist //打包生成文件的目录
  			|-src //源码所在的目录
    			|-module1.js
    			|-module2.js
    			|-module3.js
    			|-app.js //应用主源文件
		|-index.html
		|-package.json
		  {
		    "name": "browserify-test",
		    "version": "1.0.0"
		  }
	```
- 下载 browserify 第三方模块
	- 全局安装 -- npm install browserify  -g (只需要安装一次)
	- 在当前工作目录下 -- npm install browserify --save-dev
- 模块化编码
	- module1.js
		```
			module.exports = {
				foo(){
					console.log("module1");
				};
			};
		```
	- module2.js
		```
			module.exports = function(){
				console.log("module2");
			};
		```
	- module3.js
		```
			exports.foo = function(){
				console.log("module3 foo");
			};
			exports.bar = function(){
				console.log("module3 bar");
			};
		```
- 主文件引入模块
	```
		let module1 = require("./module1");
		let module2 = require("./module2");
		let module3 = require("./module3");

		module1();
		module2();
		module3.foo();
		module3.bar();
	```
- 打包处理模块文件
	`browserify js/src/app.js -o js/dist/bundle.js`
- HTML 页面引入编译后的 JS 文件
	`<script type="test/javascript" src="js/dist/bundle.js"></script>`

#### AMD
- 说明
	- Asynchronous Module Definition（异步模块定义）
	- 专门用于浏览器端，模块的加载是异步的
- 基本语法
	- 暴露模块
		- 定义没有依赖的模块
			`define(function(){return 模块})`
		- 定义有依赖的模块
			`define(['module1','module2'],function(m1,m2){return 模块})`
	- 引入模块
		- `require(['module1'],['module2'],function(m1,m2){使用})`
- 实现（浏览器）
	- HTML 页面引入  require.js 文件

##### AMD-RequireJS 模块化
- 下载`require.js`并在html页面引入
- 构建项目
	```
		|-js
			|-libs  // 用来放第三方库的文件夹
				|-require.js
  			|-modules // 用来放模块文件的文件夹
    			|-alerter.js
    			|-dataService.js
  			|-main.js // 模板主文件
		|-index.html // 页面
	```
- 编写模块
	- 定义没有依赖的模块 -- dataService.js
		```
			define(function () {
              let name = 'llc';
              function getName() {
                return name
              }
              //暴露模块
              return {getName}
		```
	- 定义没有依赖的模块 -- alerter.js
		```
			define(['dataService','jquery'],function (dataService,$) {
              let msg = 'zhiyong';
              function showMsg() {
                console.log(msg + '-' + dataService.getName());
              }
              $('body').css('background','red');
              //暴露模块
              return {showMsg}
            });
		```
- 应用主入口 -- main.js
	```
		(function () {
			require.config({
    			//基本路径
    			baseUrl: "js/",
    			//模块标识名与模块路径映射
    			paths: {
					//第三方库
					'jquery' : './libs/jquery-1.10.1',
					'angular' : './libs/angular',
					//自定义模块(在 index.html 的角度上查找路径)
					"alerter": "./modules/alerter",
					"dataService": "./modules/dataService"
				},
    			/*
     			配置不兼容AMD的模块
     			exports : 指定与相对应的模块名对应的模块对象
     			*/
				shim: {
					'angular' : {
						exports : 'angular'
      				}
    			}
			})
			//引入使用模块
			require( ['alerter', 'angular'], function(alerter, angular) {
				alerter.showMsg()
				console.log(angular);
			})
		})()
		注：引入 require 模块，需要两个参数，第一个参数 -- 传入模块名，第二个参数 -- 传入函数
	```
- 页面使用模块
	- data-main -- 指定主入口的 JS 文件
	- src -- 指定 AMD 依赖的 require.js 文件
	- `<script data-main="js/main.js" src="js/libs/require.js"></script>`

#### CMD
- 说明
	- Common Module Definition（通用模块定义）
	- 专门用于浏览器端，模块的加载是异步的
	- 模块使用时才会加载执行
- 基本语法
	- 暴露模块
		- 定义没有依赖的模块
			```
				define(function(require, exports, module){
                        exports.xxx = value,
                        module.exports = value       
                })
			```
		- 定义有依赖的模块
			```
				define(function(require, exports, module){
                	//引入依赖模块(同步)
                	var module2 = require('./module2')
                	//暴露模块
                	exports.xxx = value
                })
			```
	- 引入模块
		- `define(function(require){})`
- 实现
	- HTML 页面引入
		- `sea.js`文件
		- seajs.use() -- 指定模板主文件路径

##### CMD -- SeaJS 模块化
- 下载`sea.js` 并在 html 页面引入
- 构建项目
	```
		|-js
	    	|-libs //用来放第三方的库
	          |-sea.js
	        |-modules //用来放模块文件
	          |-module1.js
	          |-module2.js
	          |-module3.js
	          |-main.js
	    |-index.html //页面
	```
- 编写模块
	- module1.js
		```
			define(function (require,exports,module) {
              let name = 'qhf';
              function getName() {
              	  return name
              }
            
              module.exports = getName //暴露方法
            });
		```
	- module2.js
		```
			define(function (require,exports,module) {
              let module1 = require('./module1');
            
              let msg = 'llc';
              function showMsg() {
                console.log(msg + module1()); //调用module1
              }
            
              module.exports = {showMsg} //暴露对象
            });
		```
	- module3.js
		```
			define(function (require,exports,module) {
        	  exports.KEY = 'GAME KING';
            })  
		```
- 编写 main.js 主文件
	```
		define(function (require) {
           //同步引入
    	  let module2 = require('./module2');
    	  module2.showMsg() //对象调用
    
          //异步引入
          require.async('./module3',function (module3) {
      	     console.log(module3.KEY);
          })
        });
	```
- 编写 html 页面代码
	- 引入 sea.js 文件
		- `<script type="text/javascript" src="js/libs/sea.js"></script>`
	- 使用模块（指定主文件 js）
		- `<script type="text/javascript">
  seajs.use('./js/modules/main')</script>`

#### ES 6 模块
- 说明
	- 依赖模块需要编译打包处理
- 基本语法
	- 暴露模块 -- exports
		- 实际暴露的就是一个对象
	- 默认暴露 -- export default xxx
		- 可暴露任意数据，可接收任意数据
	- 引入模块 -- import xx from xx
		- 接收的变量是对象
		- 也可以对应模块名进行解构赋值
- 实现
	- 使用 Babel 将 ES6 编译成 ES5 代码
	- 使用 Browserify 编译打包 js

##### ES 6 模块化 -- ES6-Babel-Browserify
- 创建 package.json 文件
	```
		{
            "name" : "es6-babel-browserify",
            "version" : "1.0.0"
		}
	```	
- 安装 babel-cli,babel-preset-es2015 和 browserify
	- npm install babel-cli browserify -g
	- npm install babel-preset-es2015 --save-dev
	- npm install browserify --save-dev
- 创建 .babelrc 文件
	```
		{
            "presets": ["es2015"]
        }
	```
- 编写模块
	- js/src/module1.js
		```
			//分别暴露多个数据 暴露本质是一个对象
        
            export function foo() {
            	  console.log('我是foo()方法');
            }
            export function bar() {
              console.log('我是bar()方法');
            }
            
            export  let msg = 'llc';
		```
	- js/src/module2.js
		```
			//统一暴露
        
            let data = 'qhf';
            function fun1() {
            	  console.log('我是fun1方法' + '_' + data);
            }
            
            function fun2() {
            	  console.log('我是fun2方法'+ '_' +data);
            }
            
            export {fun1,fun2}
		```
	-js/src/module3.js
		```
			//默认暴露. 
			//默认接收暴露的任意数据类型. 通常是对象
        
            export  default {
              name: 'Tom',
              setName: function (name) {
                this.name = name
              }
            }
		```
- 主文件引入
	```
		//引入第三方JS库
		import $ from 'jquery'
	        
	    //引入其他模块 
		import {foo,bar} from './module1'  //解构赋值
	    import {msg} from './module1'    
	    import module2 from './module2'
	    import  obj from './module3'
	        
	    foo();
	    bar();
	    console.log(msg);
	        
	    module2.fun1();
	    module2.fun2();
	        
	    obj.setName('kobe');
	    console.log(obj);
	        
	    $('body').css('background','pink');
	```
- 编译
	- 使用 Babel 将 ES6 编译为 ES5 代码
		- babel 要转换的 js 文件的路径 -d 转换后的目标路径
		- `babel js/src -d js/lib`
	- 使用 Browserify 编译 js
		- `browserify js/lib/main.js -o js/lib/bundle.js`
- html 代码引入
	- `<script type='text/javascript' src='js/lib/bundle.js'></script>`

 