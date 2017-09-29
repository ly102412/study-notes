# JS 基本语法
### 基本语法
- 区分大小写--只针对英文
	- 全小写，首字母大写和全大写分别表达不同的含义
	    - atguigu--最多使用
        - Atguigu--最少使用
        - ATGUIGU--特殊使用
- 空格、制表符和换行的习惯
	- 作用--良好的编写习惯
- 语句后添加一个分号
    - 作用--表示当前的语句结束
    - 含义--分号是结束符
- 语句
	```
		标示符  表达式{--语句块
				语句
        }
	```
	- 语句的特点--一条语句独占一行

### JS 字面量、变量与常量
- 字面量
	- 字面量简单来说就是一个值，比如数字或者是字符串
	- 字面量都是固定的，不可变化
	- 在 JS 中可以直接使用字面量，但是不方便
- 变量
	- 变量可以用来保存字面量
	- 变量保存的值是可以发生变化的
	- 一般都是使用变量来保存一个字面量，而不是直接使用字面量
- 声明变量
	- 使用`var`为一个变量进行声明，声明后用等号连接赋值
	- 例：`var a = 123`
- 常量
	- 声明一个常量并进行赋值之后，常量的值是不允许改变的
	- 在 EMCA5 版本之前，JavaScript 是没有常量的，常量是人为规定的，没有语法结构
	- 在 EMCA5 版本之后，JavaScript 中才出现了常量的概念，其基本语法结构为 -- const 常量名 = 数据（值）

### 变量与常量的分析
#### 变量
- 当使用未赋值的变量时，浏览器控制台不会报错，会显示undefined，表示有变量但是没有值
	```
		var cda;
        console.log(cda);
	```
- 当使用未定义的变量时，报错--abc is not defined（abc未定义）
	`console.log(abc);`
 
#### 常量
- 常量被重新赋值，浏览器控制台报错--Assignment to constant variable
	```
		const STR ='呼哈偶';
       	console.log(STR);
        STR =123456;
        console.log(STR);
	```
- 重新声明一个常量，浏览器控制台报错--Identifier 'STR' has already been declared
	```
		const STR =222;
        console.log(STR);
	```
- 重新声明一个变量，浏览器控制台报错--Identifier 'STR' has already been declared
	```
		var STR =223;
        console.log(STR);
	```
- 只命名不赋值，浏览器控制台报错--Missing initializer in const declaration
	```
		const STR ;
        console.log(STR);
	```
- 不使用关键字时默认设置变量
	```
		STR =1267;
        console.log(STR);
	```
- 注：在实际工作中，变量规定使用小写，常量使用大写
                       
### 关键字与保留字
- 关键字 -- JavaScript 本身使用的一些词，不可以在开发中使用
- 保留字 -- JavaScript 目前并未有使用的一些词，以后的版本可能使用，不可以在开发中使用

### JS 标识符
- 在JS中所有可以自主命名的内容都可以认为是标识符
- 标识符的规范
	- 可以含有字母 数字 _ $，但不可以用数字开头
	- 标识符不能是 ES 标准中的关键字和保留字
	- 标识符命名时需要使用驼峰命名法
	- JS 底层保存标识符时,实际上都是使用的 unicode 编码
