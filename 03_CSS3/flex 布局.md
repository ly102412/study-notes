# flex 布局（伸缩盒模型）

### old flex
- display: -webkit-box; (移动端支持)
- 容器布局方向
	- -webkit-box-orient -- 改变主轴
	- -webkit-box-orient: vertical; 改变主轴为垂直方向（元素会垂直排列）
	- -webkit-box-orient: horizontal; 改变主轴为水平方向（元素会水平排列）
- 容器排列方向
	- -webkit-box-direction -- 改变主轴的方向（主轴默认方向是从左到右）
	- -webkit-box-direction: normal; 使用主轴默认方向显示子元素（子元素从左到右依次顺序显示）
	- -webkit-box-direction: reverse; 使用主轴反方向显示子元素（子元素从左到右依次倒序显示）
- 水平方向富裕空间管理
	- 富裕空间的管理只是用来确定富裕空间的位置. 并不给项目分配空间
	- -webkit-box-pack: center; 富裕空间在两侧
	- -webkit-box-pack: start; 主轴是 X 轴，富裕空间在右侧；主轴是 Y轴，富裕空间在下侧
	- -webkit-box-pack: end; 主轴是 X 轴，富裕空间在左侧；主轴是 Y轴，富裕空间在上侧
	- -webkit-box-pack: justify; 富裕空间平均分配到项目之间
- 垂直方向富裕空间管理
	- -webkit-box-align: center; 富裕空间在两侧
	- -webkit-box-align: start; 主轴是 X 轴，富裕空间在下侧；主轴是 Y轴，富裕空间在右侧
	- -webkit-box-align: end; 主轴是 X 轴，富裕空间在上侧；主轴是 Y轴，富裕空间在左侧
- 弹性空间管理
	- 将富裕空间按比例分配到每个项目中上. 会改变项目的空间
	- 设置在项目元素内
	- -webkit-box-flex: 1;（平均分配）

### new flex
- display: flex;
- 容器布局方向
	- flex-direction -- 改变主轴
	- flex-direction: row;  改变主轴为水平方向（元素会从左到右顺序水平排列）
	- flex-direction: column;  改变主轴为垂直方向（元素会从上到下顺序垂直排列）
- 容器排列方向
	- flex-direction: row-reverse;  沿着水平方向的反方向显示子元素（子元素从右到左依次倒序显示）
	- flex-direction: column-reverse;  沿着垂直方向的反方向显示子元素（子元素从下到上依次倒序显示）
- 水平方向富裕空间管理
	- 富裕空间的管理只是用来确定富裕空间的位置. 并不给项目增加空间
	- justify-content: center; 富裕空间在两侧
	- justify-content: flex-start; 富裕空间在主轴正方向
	- justify-content: flex-end; 富裕空间在主轴反方向
	- justify-content: space-between; 富裕空间平均分配到项目之间
	- justify-content: space-around; 富裕空间平均分配到每个项目两边（老版本没有）
- 垂直方向富裕空间管理
	- align-items: center; 富裕空间在两侧
	- align-items: flex-start; 富裕空间在侧轴正方向
	- align-items: flex-end; 富裕空间在侧轴反方向
	- align-items: baseline; 富裕空间按基线分配（老版本没有）
	- align-items: stretch; 没有高度的情况下让项目占满整个高度（老版本没有，等高布局）
- 弹性空间管理
	- 将富裕空间按比例分配到每个项目中上. 会改变项目的空间
	- 设置在项目元素内
	- flex-grow: 1;

- 新版本 flex 新增的属性
	- flex-wrap -- 控制容器为单行/列还是多行/列，并且规定了侧轴的方向，新行/列将沿着侧轴的方向堆砌
		- 值：
			- nowrap （默认值，单列/行显示）
			- wrap (多列/行)
			- wrap-reverse （侧轴反方向且多列/行显示）
		- 不可继承
	- flex-flow -- 是“flex-direction”和“flex-wrap”的简写，控制主轴和侧轴的位置、方向以及是否多行/列显示
		- 默认值：row nowrap
		- 不可继承
	-  align-content -- 定义容器侧轴上有额外空间时，如何排布每一行/列（只有一行/列时无用）
		-  值：
			-  stretch（默认值，剩余空间平均分配给每一行/列）
			-  flex-start（所有行/列从侧轴起点开始排列，后一行/列排在前一行/列下）
			-  flex-end（所有行/列从侧轴末尾开始排列，后一行/列排在前一行/列下）
			-  center（所有行/列从侧轴中心开始排列，后一行/列排在前一行/列下）
			-  space-between（所有行/列在容器中平均分布，相邻两行/列间距相等，只在各个项目之间分配）
			-  space-around（所有行/列在容器中平均分布，相邻两行/列间距相等，给项目两边同时分配富裕空间）
	- order -- 规定了容器中的可伸缩项目在布局时的顺序。元素按照 order 属性的值的增序进行布局。拥有相同 order 属性值的元素按照它们在源代码中出现的顺序进行布局
		- 0（默认值）
		- 不可继承
	- align-self -- 单独控制某一元素富裕空间分配的位置
	- flex-grow -- 定义弹性盒子项的拉伸因子
	- flex-shrink -- 指定了 flex 元素的收缩规则  默认值为1
	- flex-basis -- 指定了 flex 元素在主轴方向上的初始大小
	- flex -- 是 flex-grow，flex-shrink，flex-basis 的简写属性
- 平均分配
	- flex:1;
	- 等同于 `flex-grow: 1;flex-shrink: 1;flex-basis: 0;`

### flex 等分布局

		<!DOCTYPE html>
		<html>
			<head>
				<meta charset="UTF-8">
				<title></title>
				<style type="text/css">
					*{
						margin: 0;
						padding: 0;
					}
			
					#wrap{
						display: -webkit-box;
						display: flex;
						width: 400px;
						height: 200px;
						border: 1px solid;
						margin: 0 auto;
					}
					#wrap .item{
						-webkit-box-flex: 1;
						flex-grow:1 ;
						flex-basis: 0;
						width: 0;
						background: pink;
						height: 50px;
					}
				</style>
			</head>
			<body>
				<div id="wrap">
					<div class="item">1</div>
					<div class="item">22</div>
					<div class="item">33</div>
					<div class="item">4</div>
					<div class="item">555</div>
				</div>
			</body>
		</html>
