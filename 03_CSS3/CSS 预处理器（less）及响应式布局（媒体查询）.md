# CSS 预处理器 -- less

### less
- less 是一种动态样式语言，属于css预处理器的范畴，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展。

### less编译工具
- koala 官网:www.koala-app.com 
	
### less中的注释
- 以//开头的注释，不会被编译到css文件中
- 以/**/包裹的注释会被编译到css文件中  
	
### less中的变量
- 使用@来申明一个变量：@pink：pink;
	- 作为普通属性值只来使用：直接使用@pink
	- 作为选择器和属性名：#@{selector的值}的形式
	- 作为URL：@{url}
	- 变量的延迟加载

### less中的嵌套规则
- 基本嵌套规则
- &的使用

### less中的混合
- 混合就是将一系列属性从一个规则集引入到另一个规则集的方式
	- 普通混合      
	- 不带输出的混合
	- 带参数的混合
	- 带参数并且有默认值的混合
	- 带多个参数的混合
	- 命名参数
	- 匹配模式
	- arguments变量
	
### less运算
- 在less中可以进行加减乘除的运算

# 响应式布局 -- 媒体查询

### 媒体类型
- all -- 所有媒体
- braille -- 盲文触觉设备
- embossed -- 盲文打印机
- print -- 手持设备
- projection -- 打印预览
- screen -- 彩色屏幕
- speech -- “听觉”类似的媒体设备

### 媒体特性
- min-width -- 分辨率宽度大于设置值的时候识别
- max-width -- 分辨率宽度小于设置值的时候识别
- orientation：portrait -- 竖屏
- orientation：landscape -- 横屏
- min-device-pixel-ratio -- 像素比

### 关键字
- and -- 连接媒体特性 
- not -- 排除指定媒体类型
- only -- 指定某种特定的媒体类型

### 语法
- @media + 关键字 + 媒体类型 + and + (媒体特性) {}

# less 及 媒体查询的综合应用
- 一物理像素
	- HTML 代码
	```
		<!DOCTYPE html>
		<html>
			<head>
				<meta charset="UTF-8">
				<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no"/>
				<link rel="stylesheet" type="text/css" href="css/mixin.css"/>
				<title></title>
			</head>
			<body>
				<div id="wrap">
			
				</div>
			</body>
		</html>
	```
	- less 代码
	```
		*{
			margin: 0;
		    padding: 0;
		}
		//一物理像素的
		//上边框
		.onePx(@_,@c:black){
			position: relative;
			&:before{
				position: absolute;
		        content: "";
		        display: block;
		        width: 100%;
		        height: 1px;
				@media only screen and (-webkit-min-device-pixel-ratio:2 ){
					transform: scaleY(.5);
				}
				@media only screen and (-webkit-min-device-pixel-ratio:3 ){
					transform: scaleY(.33333333333);
				}
			}
		}
		.onePx(top,@c:black){
			&:before{
        		top: 0;
        		background: @c;
    		}
		}
		.onePx(bottom,@c:black){
    		&:before{
        		bottom: 0;
        		background: @c;
    		}
		}
		#wrap{
			.onePx(top);
			width: 100px;
		    height: 100px;
			background: pink;
			margin: 50px;
		}

	```
	- 编译后的 CSS 代码
	```
		* {
			margin: 0;
		  	padding: 0;
		}
		#wrap {
			position: relative;
			width: 100px;
			height: 100px;
			background: pink;
			margin: 50px;
		}
		#wrap:before {
		    position: absolute;
		  	content: "";
		  	display: block;
		  	width: 100%;
		  	height: 1px;
		}
		@media only screen and (-webkit-min-device-pixel-ratio: 2) {
		  	#wrap:before {
				transform: scaleY(0.5);
		  	}
		}
		@media only screen and (-webkit-min-device-pixel-ratio: 3) {
		  	#wrap:before {
		    	transform: scaleY(0.33333333);
		  	}
		}
		#wrap:before {
		  	top: 0;
		  	background: #000000;
		}
	```
