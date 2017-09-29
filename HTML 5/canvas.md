# Canvas
### Canavs 基础内容
#### Canvas 技术允许在 HTML 页面直接绘制图形
- 不再需要引入外部图片（图形），HTML 页面性能有所提高
- 可以实现一些比较复杂的图形绘制工作

#### Canvas 技术主要应用方向
- Web 应用方面主要实现图表类
- 网页游戏方面 - 主要实现 2D 效果

#### HTML 5 提供有关图形方面的技术
-  Canvas -- 主要以 2D 为主
-  WebGL -- 主要以 3D 为主
-  SVG -- 矢量图

#### Canvas 的特点
- 绘制的图形与 HTML 页面之间是无关系的
- 通过 Canvas 绘制的图形不能使用 DOM API
- 通过 Canvas 绘制的图形不能绑定事件
- Canvas 画布最终是以图片（png/jpg）形式出现
- 绘制图形默认的颜色为黑色

### 如何使用 Canvas 画布
#### 在 HTML 页面中定义`<canvas>`元素
- 设置`<canvas>`元素宽度和高度使用属性方式
- 使用 CSS 样式方式或属性方式设置`<canvas>`元素的高度和宽度
- 代码展示
	```
		<!--
			在HTML页面中,定义<canvas>元素
			* 默认只定义<canvas>元素时
				* 效果非常类似于<div>元素,但不一样的地⽅方:
					* <div>元素在默认情况下,不具有高度和宽度
					* <canvas>元素在默认情况下,具有高度和宽度的
						* 宽度 - 300px
						* 高度 - 150px
			* 设置<canvas>元素的高度和宽度
				* (建议)使用属性width和height
				* 使用CSS中的属性width和height
					* 绘制的图形会被拉伸
		-->
		<canvas id="canvas" width="500px" height="500px" style="background:pink;"></canvas>
		<!--
		<canvas id="canvas" style="width:500px;height:500px;"></canvas>
		-->
	```

#### 在 JS 代码中实现
- 获取`<canvas>`元素
- 通过`<canvas>`元素，创建画布对象
	- getContext（'2d'）函数
	- 返回画布对象
- 利用画布对象进行图形的绘制
- 代码展示
	```
		// 获取HTML⻚页⾯面中的<canvas>元素
		var canvas = document.getElementById("canvas");
		/*
			通过<canvas>元素,创建画布对象
			使⽤用getContext(type)函数,创建画布对象
			* 该函数返回画布对象
			* type参数
				* 设置当前创建的画布是2d还是3d
				* 注意
					* 参数选项是2d(3d效果使用WebGL)
					* 必须写成"2d"
		*/
		var context = canvas.getContext("2d");
		// 利利⽤用画布对象,进行绘制图形
		context.fillRect(10,10,100,100);
	```

### 绘制图形
#### 绘制矩形
- 绘制实心（填充）矩形
	- 代码实现
		- `fillRect(x,y,width,height)`
	- 参数
		- x 和 y -- 绘制矩形的左上角的坐标值
		- width -- 设置绘制矩形的宽度（单位为px）
		- height -- 设置绘制矩形的高度（单位为px）
- 绘制空心（描边）矩形
	- 代码实现
		- `strokeRect(x,y,width,height)`
	- 参数
		- x 和 y -- 绘制矩形的左上角的坐标值
		- width -- 设置绘制矩形的宽度（单位为px）
		- height -- 设置绘制矩形的高度（单位为px）
- 清楚制定区域的矩形
	- 代码实现
		- `clearRect(x,y,width,height)` 
	- 参数
		- x 和 y -- 绘制矩形的左上角的坐标值
		- width -- 设置绘制矩形的宽度（单位为px）
		- height -- 设置绘制矩形的高度（单位为px）
-  代码实现
	```
		<canvas id="canvas" width="500px" height="500px"></canvas>
		<script>
			// 1. 获取<canvas>元素
			var canvas = document.getElementById("canvas");
			// 2. 创建画布对象
			var context = canvas.getContext('2d');
			// 3. 绘制图形
			// a. 绘制实心矩形
			context.fillRect(10,10,100,100);
			// b. 绘制空心矩形
			context.strokeRect(120,10,100,100);
			// c. 清除指定区域的矩形
			context.fillRect(230,10,100,100);
			context.clearRect(240,20,80,80);
		</script>
	```

#### 设置样式
- 属性
	- fillStyle -- 设置填充样式
	- strokeStyle -- 设置描边样式
	- globalAlpha -- 设置透明度（0-1）
- 注
	- 一定要先设置样式（颜色），再绘制图形
	- 每次改变样式（颜色），需重新设置
- 代码实现
	```
		<canvas id="canvas" width="500px" height="500px"></canvas>
		<script>
			var canvas = document.getElementById("canvas");
			var context = canvas.getContext('2d');
			// a. 设置填充样式
			context.fillStyle = "pink";
			// b. 绘制实心矩形
			context.fillRect(10,10,100,100);
			context.fillStyle = "blue";
			context.fillRect(10,120,100,100);
			// 设置描边样式
			context.strokeStyle = "red";
			context.strokeRect(120,10,100,100);
			context.strokeStyle = "green";
			context.strokeRect(120,120,100,100);
			// 设置透明度
			context.globalAlpha = 0.5;
			context.fillRect(230,10,100,100);
			context.fillStyle = "black";
			context.globalAlpha = 0.1;
			context.fillRect(230,120,100,100);
		</script>
	```

#### 设置渐变
- 线性渐变
	- 线性渐变主要依靠基准线，所谓基准线就是设置线性渐变的标准
	- 代码实现
		- `createLinearGradient(x1,y1,x2,y2)`
	- 参数
		- x1 和 y1 -- 基准线的起点坐标值
		- x2 和 y2 -- 基准线的终点坐标值
	- 代码实现
		```
			<canvas id="canvas" width="500px" height="500px"></canvas>
			<script>
				var canvas = document.getElementById("canvas");
				var context = canvas.getContext('2d');
				/*
				设置线性渐变
				createLinearGradient(x1,y1,x2,y2)⽅方法
				* 该方法具有返回值,是渐变对象
				*/
				var grd = context.createLinearGradient(0,0,100,100);
				/*
					设置线性渐变的颜色和位置
					addColorStop(position,color)
					* position - 设置颜色的位置
						* 值的范围为 0 - 1
					* color - 设置颜色
				*/
				grd.addColorStop(0,"red");
				grd.addColorStop(1,"blue");
				grd.addColorStop(0.5,"yellow");
				// 将设置的线性渐变,赋值给样式(fillStyle和strokeStyle)
				context.fillStyle = grd;
				// 绘制矩形
				context.fillRect(0,0,100,100);
			</script>
		```
- 射线（扇形）渐变
	- 线性渐变主要依靠基准圆，所谓基准圆就是设置线性渐变的标准
	- 代码实现
		- `createRadialGradient(x1,y1,r1,x2,y2,r2)`
	- 参数
		- x1 和 y1 -- 基准线的起点坐标值
		- r1 -- 第一个基准圆的半径
		- x2 和 y2 -- 基准线的终点坐标值
		- r2 -- 第二个基准圆的半径
	- 代码实现
		```
			<canvas id="canvas" width="500px" height="500px"></canvas>
			<script>
				var canvas = document.getElementById("canvas");
				var context = canvas.getContext("2d");
				/*
					设置射线渐变
					createRadialGradient(x1,y1,r1,x2,y2,r2)
					* 该方法返回渐变对象
				*/
				var grd = context.createRadialGradient(100,100,100,canvas.width,canvas.height,200);
				/*
				设置渐变颜色
				*/
				grd.addColorStop(0,"red");
				grd.addColorStop(1,"blue");
				// 将渐变对象赋值给样式
				context.fillStyle = grd;
				// 绘制矩形
				context.fillRect(0,0,canvas.width,canvas.height);
			</script>
		``` 
- 设置渐变颜色
	- 代码实现
		`addColorStop(position,color)`
	- 参数
		- position -- 设置渐变颜色的位置，值的范围必须是 0-1
		- color -- 设置渐变的颜色

#### 绘制文字
- 属性
	- font -- 设置文字的属性（用法同 CSS 属性 font）
	- textAlign -- 水平对齐方式（left：基准线在左边；center：基准线在中间；right：基准线在右边）
	- textBaseline -- 垂直对齐方式（top：基准线在上边；middle：基准线在中间；bottom：基准线在下边；hanging：悬挂基准线；alphabetic：字母基线）
- 绘制实心文字
	- 代码实现
		`fillText(text，x，y)`
	- 参数
		- text -- 绘制的文字内容
		- x 和 y -- 绘制文字的坐标值
- 绘制空心文字
	- 代码实现
		`strokeText(text,x,y)`
	- 参数
		- text -- 绘制的文字内容
		- x 和 y -- 绘制文字的坐标值
- 实例代码
	```
		<canvas id="canvas" width="500px" height="500px"></canvas>
		<script>
			var canvas = document.getElementById("canvas");
			var context = canvas.getContext('2d');
			
			// 设置文字样式
			context.font = "bold 48px 宋体";
			// 基准线
			context.beginPath();
			context.moveTo(100,0);
			context.lineTo(100,400);
			context.stroke();
			// 设置水平对齐
			context.textAlign = "right";
			// 绘制文字
			context.fillText("text",100,50);
			
			// 设置水平对齐
			context.textAlign = "center";
			// 绘制文字
			context.fillText("text",100,100);
			
			// 设置水平对齐
			context.textAlign = "left";
			// 绘制文字
			context.fillText("text",100,150);
			// 基准线
			context.beginPath();
			context.moveTo(0,300);
			context.lineTo(500,300);
			context.stroke();

			// 设置垂直对齐
			context.textBaseline = "top";
			context.strokeText("text",0,300);

			context.textBaseline = "middle";
			context.strokeText("text",100,300);

			context.textBaseline = "bottom";
			context.strokeText("text",200,300);

			context.textBaseline = "hanging";
			context.strokeText("text",300,300);

			context.textBaseline = "alphabetic";
			context.strokeText("text",400,300);
		</script>
	```

#### 设置阴影
- 属性
	- shadowColor -- 设置阴影颜色
	- shadowOffsetX -- 设置水平方向阴影
	- shadowOffsetY -- 设置垂直方向阴影
	- shadowBlur -- 设置阴影程度

### 创建路径
- 图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。一个路径，甚至一个子路径，都是闭合的。使用路路径绘制图形需要一些额外的步骤
	- 首先，需要创建路径起始点。
	- 然后，使用画图命令去画出路径。
	- 之后，把路径封闭。
	- 一旦路径生成，你就能通过描边或填充路路径区域来渲染图形

#### 绘制矩形
- 绘制矩形的实现步骤
	- 调用 beginPath() 方法
	- 使用 rect（x,y,width,height）方法，设置矩形的坐标值及宽度和高度
	- 通过 fill() 或 stroke() 方法进行绘制
- 使用方法说明
	- `rect(x,y,width,height)`
- 参数
	- x 和 y -- 表示矩形的左上角坐标值
	- width 和 height -- 表示矩形的宽度和高度

#### 绘制圆形
- 绘制圆形的实现步骤
	- 调用 beginPath() 方法，创建新建一条路径
	- 使用 arc(x, y, radius, startAngle, endAngle, anticlockwise) 方法，设置矩形的坐标值及宽度和高度
	- 通过 fill() 或 stroke() 方法进行绘制
- 使用方法
	- `arc(x, y, radius, startAngle, endAngle, anticlockwise)`
- 参数
	- x 和 y -- 表示圆形的圆心坐标值
	- radius -- 表示圆形的半径
	- startAngle -- 表示绘制圆形的开始点，值为 0
	- endAngle -- 表示绘制圆形的结束点，值为 Math.PI*2
	- anticlockwise -- 表示是以顺时针还是逆时针方式绘制圆形，Boolean 值（默认值为 false，表示顺时针）

#### 绘制弧形
- 绘制圆形的实现步骤
	- 调用 beginPath() 方法，创建新建一条路径
	- 使用 arc(x, y, radius, startAngle, endAngle, anticlockwise) 方法，设置矩形的坐标值及宽度和高度
	- 通过 fill() 或 stroke()方法进行绘制
- 使用方法说明
	- `arc(x, y, radius, startAngle, endAngle, anticlockwise)`
- 参数
	- x 和 y -- 表示圆形的圆心坐标值
	- radius -- 表示圆形的半径
	- startAngle -- 表示绘制圆形的开始点（取值范围：0至 Math.PI*2）
	- endAngle -- 表示绘制圆形的结束点（取值范围：0至 Math.PI*2）
	- anticlockwise -- 表示是以顺时针还是逆时针方式绘制圆形，Boolean 值（默认值为 false，表示顺时针）
- 注
	- 如果绘制的是空心弧形的话，在 arc() 方法调用后
		-  如果使用 closePath() 方法的话，绘制的图形会自动将终点和起点连接成线
		-  如果不用 closePath() 方法的话，绘制的图形会呈现开口状

#### 绘制直线
- 调用 beginPath() 方法，创建一条路径
- 使用 moveTo(x,y) 方法，设置直线的起点坐标值
- 使用 lineTo(x,y) 方法，设置直线的终点坐标值
- 通过 stroke() 方法进行绘制

#### 绘制折线
- 使用 beginPath() 方法，创建一条路径
- 使用 moveTo(x,y) 方法，设置直线的起点坐标值
- 使用 lineTo(x,y) 方法，设置直线的终点坐标值
- 通过 stroke() 方法进行绘制
- 注：在绘制折线时，lineTo() 方法既可以绘制折点，也可以绘制终点

#### 绘制多边形
- 调用 beginPath() 方法，创建一条路径
- 使用 moveTo() 方法，设置直线的起点坐标值
- 使用 lineTo() 方法，设置直线的终点坐标值
- 调用 closePath() 方法，闭合当前绘制的路径
- 通过 fill() 或 stroke() 方法进行绘制

### 设置线型
#### 设置线宽
- lineWidth：指定线条的粗细，默认值是 1.0
- 实例代码
	```
		<canvas id="myCanvas" width="578" height="200"></canvas>
		<script>
			var canvas = document.getElementById('myCanvas');
			var context = canvas.getContext('2d');
			context.beginPath();
			context.moveTo(100, 150);
			context.lineTo(450, 50);
			context.lineWidth = 15;
			context.stroke();
		</script>
	```

#### 设置端点的形状
- lineCap：指定线条端点的形状
	- butt：默认，向线条的每个末端添加平直的边缘
	- round：向线条的每个末端添加圆形线帽
	- square：向线条的每个末端添加正方向线帽
- 注：round 和 square 会使线条稍微变长
- 实例代码
	```
		<canvas id="myCanvas" width="578" height="200"></canvas>
		<script>
			var canvas = document.getElementById('myCanvas');
			var context = canvas.getContext('2d');

			// butt line cap (top line)
			context.beginPath();
			context.moveTo(200, canvas.height / 2 - 50);
			context.lineTo(canvas.width - 200, canvas.height / 2 - 50);
			context.lineWidth = 20;
			context.strokeStyle = '#0000ff';
			context.lineCap = 'butt';
			context.stroke();

			// round line cap (middle line)
			context.beginPath();
			context.moveTo(200, canvas.height / 2);
			context.lineTo(canvas.width - 200, canvas.height / 2);
			context.lineWidth = 20;
			context.strokeStyle = '#0000ff';
			context.lineCap = 'round';
			context.stroke();
			
			// square line cap (bottom line)
			context.beginPath();
			context.moveTo(200, canvas.height / 2 + 50);
			context.lineTo(canvas.width - 200, canvas.height / 2 + 50);
			context.lineWidth = 20;
			context.strokeStyle = '#0000ff';
			context.lineCap = 'square';
			context.stroke();
		</script>
	```

#### 设置交点形状
- lineJoin：指定两条线之间的连接点的形状
	- round：创建圆角
	- bevel：创建斜角
	- miter：默认，创建尖角
- miterLimit：与 lineJoin 一起使用，当 lineJoin 设置为 miter 时，可用于确定线条交接点的延伸范围
- 实例代码
	```
		<canvas id="myCanvas" width="578" height="200"></canvas>
		<script>
			var canvas = document.getElementById('myCanvas');
			var context = canvas.getContext('2d');
			
			// set line width for all lines
			context.lineWidth = 25;

			// miter line join (left)
			context.beginPath();
			context.moveTo(99, 150);
			context.lineTo(149, 50);
			context.lineTo(199, 150);
			context.lineJoin = 'miter';
			context.stroke();

			// round line join (middle)
			context.beginPath();
			context.moveTo(239, 150);
			context.lineTo(289, 50);
			context.lineTo(339, 150);
			context.lineJoin = 'round';
			context.stroke();

			// bevel line join (right)
			context.beginPath();
			context.moveTo(379, 150);
			context.lineTo(429, 50);
			context.lineTo(479, 150);
			context.lineJoin = 'bevel';
			context.stroke();
		</script>
	```

### 处理图像
- 在 HTML 5 中，不仅可以使用 Canvas API 来绘制图形，还可以读取磁盘或网络中的图像文件，然后使用 Canvas API 将该图像绘制在画布中

#### 绘制图像
- 加载图像
	- 使用相同页面中的图片
	- 使用相同页面中的其他 Canvas 元素
	- 可以通过脚本 Image() 构造函数创建图像
- 绘制图像
	- 使用 drawImage() 方法绘制图像
	- 方法一
		- `drawImage(img, x, y)`
		- 参数
			- img -- 需要绘制的图像
			- x 和 y -- 绘制图像的坐标值
	- 方法二
		- `drawImage(img, x, y, width, height)`
		- 参数
			- img -- 需要绘制的图像
			- x 和 y -- 绘制图像的坐标值
			- width 和 height -- 设置绘制图像的宽度和高度
	- 实例代码
		```
			<canvas id="myCanvas" width="578" height="400"></canvas>
			<script>
				var canvas = document.getElementById('myCanvas');
				var context = canvas.getContext('2d');
				var imageObj = new Image();
				imageObj.src = 'darth-vader.jpg';
				imageObj.onload = function() {
				context.drawImage(imageObj, 69, 50);
				};
			</script>
		```
	- 注：若调用 drawImage 时，图片没加载完，那什么都不会发生（在一些旧的浏览器中可能会抛出异常），因此需要使用 img.onload 来保证不会在加载完毕之前就使用这个照片
	- 实例代码
		```
			var img = new Image(); // 创建img元素
			img.src = 'myImage.png'; // 设置图片源地址
			img.onload = function(){
				// 执行drawImage语句
			}
		```

#### 平铺图像
- 所谓平铺图像就是用按一定比例缩小后的图像将画布填满
	- 加载图像
	- 通过 createPattern(img,type) 方法设置平铺的方式
	- 将平铺对象赋值给 fillStyle 或 strokeStyle 属性
	- 将平铺的图像进行绘制
	- 代码
		`createPattern(img, type)`
	- 参数
		- img -- 需要平铺的图像
		- type -- 平铺方式（no-repeat：不平铺；repeat-x：水平方向平铺；repeat-y：垂直方向平铺；repeat：全方向平铺）
	- 实例代码
		```
			<canvas id="myCanvas" width="578" height="200"></canvas>
			<script>
				var canvas = document.getElementById('myCanvas');
				var context = canvas.getContext('2d');
				var imageObj = new Image();
				imageObj.src = 'wood-pattern.png';
				imageObj.onload = function() {
				var pattern = context.createPattern(imageObj, 'repeat');
				context.rect(0, 0, canvas.width, canvas.height);
				context.fillStyle = pattern;
				context.fill();
				};
			</script>
		```
	- 注：若调用 drawImage 时，图片没加载完，那什么都不会发生（在一些旧的浏览器中可能会抛出异常），因此需要使用 img.onload 来保证不会在加载完毕之前就使用这个照片
	- 实例代码
		```
			var img = new Image(); // 创建img元素
			img.src = 'myImage.png'; // 设置图片源地址
			img.onload = function(){
				// 执行drawImage语句
			}
		``` 

#### 切割图像
- 调用 beginPath() 方法，创建一条路径
- 使用 rect() 或 arc() 方法
- 通过 clip() 方法进行切割
- 实例代码
	```
		<canvas id="canvas" width="578" height="200"></canvas>
		<script>
			var canvas = document.getElementById('canvas');
			var context = elem.getContext('2d');
			var image=new Image();
			image.src="img/flower.jpg";
			image.onload=function(){
			context.drawImage(image,0,0,280,190);
			}
			context.beginPath();
			context.arc(140,95,60,0,Math.PI*2,true);
			context.closePath();
			context.clip();
		</script>
	```

#### 画布方法
- 状态方法
	- save() -- 保存当前画布的属性、状态
	- restore() -- 恢复画布的属性、状态
	- 实例代码
		```
			<canvas id="canvas" width="578" height="200"></canvas>
			<script>
				var ctx = document.getElementById('canvas').getContext('2d');
	
				ctx.fillRect(0,0,150,150); // Draw a rectangle with default settings
				ctx.save(); // Save the default state
	
				ctx.fillStyle = '#09F' // Make changes to the settings
				ctx.fillRect(15,15,120,120); // Draw a rectangle with new settings
	
				ctx.save(); // Save the current state
				ctx.fillStyle = '#FFF' // Make changes to the settings
				ctx.globalAlpha = 0.5;
				ctx.fillRect(30,30,90,90); // Draw a rectangle with new settings
	
				ctx.restore(); // Restore previous state
				ctx.fillRect(45,45,60,60); // Draw a rectangle with restored settings
	
				ctx.restore(); // Restore original state
				ctx.fillRect(60,60,30,30); // Draw a rectangle with restored settings
			</script>
		```
- 转换方法
	- translate(x, y) ：用来移动 canvas 和它的原点到一个不不同的位置
		- x 是左右偏移量
		- y 是上下偏移量
	- scale(x, y) ：用它来增减图形在 canvas 中的像素数目，对形状、位图进行缩小或者放大
		- x,y 分别是横轴和纵轴的缩放因子，它们都必须是正值
		- 值分类：
			- 值比 1.0 小表示缩小
			- 值比 1.0 大表示放大
			- 值为 1.0 时什么效果都没有
	- rotate(angle) ：用于以原点为中心旋转 canvas
		- 旋转的角度(angle)，它是顺时针方向的，以弧度为单位的值