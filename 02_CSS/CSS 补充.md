# CSS 补充
### 定位和浮动的补充
#### 包含块和定位
- 定位的参照物其实就是包含块
- 根元素的包含块也称初始包含块(由用户代理:浏览器)
	- 初始包含块是一个视窗大小的矩形(定位参照)
	- 位置以及大小默认和视窗一样但不代表就是视口
	- 根元素不是 html 元素就是 body 元素
- 非根元素的相对定位或无定位时的包含块就是离它最近嵌套的块级元素
	- 如果没有,则包含块就是初始包含块
- 非根元素的绝对定位的包含块就是离它最近嵌套的开启了定位的块级元素
	- 从块级元素的 padding 区域开始排列
	- 如果没有,则包含块就是初始包含块
- margin 和 padding 取百分比都是从包含块内容区的 width 中获取

#### 浮动
- 最初用作图片的环绕
- 浮动元素的包含块是离它最近的块级祖先元素
- 浮动时要考虑提升层级分为两级
	- 文字
	- 盒模型 (浮动只提升半级)
- 其他情况下,层级提升只有一级 (盒模型)

----

### overflow
#### 参数
- visible -- 默认值，内容不会被修剪，会呈现在元素框之外
- hidden	 -- 内容会被修剪，并且其余内容是不可见的
- scroll	 -- 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容
- auto -- 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容

#### html 和 body 的 overflow
- html 元素或 body 元素中有且只有一个有 overflow 属性时,这个属性会传给上一层 document 身上
- 当且仅当 html 和 body 都存在 overflow 属性时
	- body 的 overflow 属性会作用于 body 自身上
	- html 的 overflow 属性会作用于上一层 document 身上

#### 禁止系统滚动条且 html，body 和视口高度三合一
```
	html,body{
      /*禁止系统滚动条. 并且把html body 和视口高度三合一*/
      overflow: hidden; 
      height: 100%;
	}
```
-----

### 绝对定位模拟固定定位
#### 原理与实现方法
- 解决固定定位因为浏览器兼容性或移动端浏览器造成的失效问题
- 实现方法:
	- 首先禁止系统滚动条
	- html 和 body 都有 overflow 属性时,把滚动条加给 body
	- 然后让 body 充满整个屏幕且必须把 html 和 body 的 height 都设置100%
	- 此时滚动条就看上去是系统的了，然后再用绝对定位模拟固定定位
- 实现原理: 
	- 只有系统滚动条才会移动初始包含块，所以把滚动条放到 body 身上
	- 当 body 上的滚动条移动时初始包含块不会移动，只是body里的内容移动
	- 当初始包含块不会被移动时, 那么基于初始包含块绝对定位的元素也就不会被移动

#### 滚动条与初始包含块
- 系统滚动条未出现时, 初始包含块的大小和位置跟视口一模一样
- 系统滚动条出现时, 移动系统滚动条会让初始包含块的位置发生变化, 而视口永远不会动

#### 代码实现
```
	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="UTF-8">
	  <title>Title</title>
	  <style type="text/css">
	    * {
	      margin: 0;
	      padding: 0;
	    }
	
	    /*1. 禁止系统滚动条*/
	    html,body{
	      overflow: hidden;
	      height: 100%;
	    }
	
	    /*2. body出现滚动条模拟固定定位*/
	    body{
	      /*margin: 30px;*/
	      border: 1px solid red;
	      overflow: auto;
	      height: 100%;
	    }
	
	    #test{
	      position: absolute;
	      left: 50px;
	      top: 50px;
	
	      width: 200px;
	      height: 200px;
	      background: greenyellow;
	    }
	  </style>
	</head>
	<body>
	  <div id="test"></div> <!-- 模拟固定定位 -->
	  <div style="height: 30000px"></div> <!-- 模拟滚动条-->
	</body>
	</html>
```
----------
### 底部粘贴布局
#### 需求
- footer始终固定在底部 (移动端常用)

#### 实现原理
- 必须要有外层包裹元素，显示的内容区要在包裹元素内，底部footer要在包裹元素的外部
- 由于 footer 始终要在底部且靠外层包裹元素高度支撑所以要给外层包裹元素设置高度 100% 且最小高度等于视口高度
- 由于继承要一级一级实现,所以 html 和 body 都要设置 height 为100%
- 由于外层包裹元素高度为视口高度，footer 要显示出来必须要设置等同于自身高度负外边距 margin-top
- 当内容区的内容过多时会发生重叠情况，还要给内容区设置留白区域等同于 footer 自身高度的 padding 值
- footer 位置始终靠外层包裹元素高度来支撑，所以外层包裹元素还需要清除浮动确保高度始终被子元素撑开

#### 代码实现
```
	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="UTF-8">
	  <meta name="viewport" content="width=device-width,initial-scale=1.0">
	  <title>Title</title>
	  <style type="text/css">
	    * {
	      margin: 0;
	      padding: 0;
	    }
	
	    html,body{
	      overflow: hidden;
	      height: 100%;
	    }
	
		/*外层包裹元素*/
	    #warp{
	      height: 100%; /*3.高度必须一级一级拿下来.否则无法继承*/
	      min-height: 100%;/*2.最小高度等于视口高度. 给外层包裹元素*/
	    }
	
	    /*内容区*/
	    #main{
	      line-height: 30px;
	      background: blue;
	      text-align: center;
		/*5.由于内容溢出会覆盖底部. 所以应该给内容区添加一个留白区*/
	      padding: 30px;
	    }
	
	    /*底部*/
	    #footer{
	      height: 30px;
	      background: yellow;
	      text-align: center;
		/*4.负外边距 footer上来固定在底部*/
	      margin-top: -30px; 
	    }
	
	    /*6.footer位置始终靠warp高度来支撑. 最好给warp清除浮动确保高度始终被子元素撑开*/
	    .clearfix{
	      *zoom: 1;
	    }
	    .clearfix:after{
	      content:'';
	      display: block;
	      clear: both;
	    }
	  </style>
	</head>
	<body>
	
	<!--CSS选择器从右往左读性能最好-->
	  <div id="warp" class="clearfix">
	    <div id="main">
	      <!--1.必须要有包裹元素. 显示的内容要在包裹元素内. 底部要在包裹元素外部-->
	      <h4>main</h4> <br>
	      <h4>main</h4> <br>
	      <h4>main</h4> <br>
	      <h4>main</h4> <br>
	      <h4>main</h4> <br>
	      <h4>main</h4> <br>
	    </div>
	  </div>
	  <div id="footer">footer</div>
	</body>
	</html>
```
-----
### 文本出现省略号
- 处理的元素首先是块元素
- 截断多余部分
- 设置文本不换行
- 文本溢出时出现省略号
- 代码实现
	```
		display: block;
	    overflow: hidden;
	    white-space: nowrap;
	    text-overflow: ellipsis;
	```
----
### 2d 组合变化
- 执行顺序: 从右往左
- 只认最初点和最终点，并以组合变换形式进行变换
- 当 translate 位移在最左时, 位移位置不受变化
- 当 translate 位移在最右时, 位移位置受矩阵计算影响
- transform 多组合有 rotate 切换时, 变换个数和变换种类以及书写顺序必须一致，否则过渡会失效
