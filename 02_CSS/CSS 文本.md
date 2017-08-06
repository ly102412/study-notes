# CSS 文本

### color 设置字体颜色
- rgba（255，0，0，.8）
	- a 代表不透明度

### direction 设置文本方向
- 块元素 -- direction 不改变书写顺序
- 行内元素 -- direction 不改变书写顺序
- 行内块元素 -- 会改变文本的排列位置

### text-align 设置文本对齐方式
- 规定一行中文本内容，行内元素，行内块元素的对齐方式
	- left  把文本排列到左边。默认值：由浏览器决定。
	- right把文本排列到右边。 
	- center  把文本排列到中间。
	- justify  实现两端对齐文本效果。本质是“拉伸了空白”的距离
	- 可继承

### text-decoration 向文本添加修饰
- none 默认值。定义标准的文本。可取消a链接默认下划线
- underline 添加下划线
- overline 上加线
- line-through 中划线
- 可继承

### text-indent 首行缩进
- length  定义固定的缩进。默认值：0。单位px 
- % 	      定义基于父元素宽度的百分比的缩进。
- 可继承
- 注意: 实际开发中我们使用em，确保一个正确的比例!! 1em=16px

### text-transform 控制元素中的字母
- none 默认值。定义带有小写字母和大写字母的标准的文本。
- capitalize   文本中的每个单词以大写字母开头。
- uppercase  定义仅有大写字母。
- lowercase   定义仅有小写字母。
- 可继承

### letter-spacing 设置字符间距
- normal  默认值,相当于0。规定字符间没有额外的空间。
- length   定义字符间的固定空间（允许使用负值）。单位px 
- 可继承

### word-spacing 设置字间距
- normal  默认值,相当于0。规定字符间没有额外的空间。
- length   定义字符间的固定空间（允许使用负值）。单位px 
- 可继承

### white-space 设置元素中空白的处理方式
- 文字用于换行 -- white-space：nowrap
- 省略号的处理
	```
	white-space：nowrap；
    text-overflow：ellipsis；
    overflow：hidden；
    display：block；
	```
- 可继承

### line-height 行高
- 定义了该元素中基线之间最小距离
- 行高 = 字体大小 + 行间距
- 当 line-height 的值等于 height 时，文本、行内元素、行内块元素会垂直居中
	- normal 默认
    - number 设置数字大小.会与当前字体尺寸相乘来设置行间距
    - length 设置固定的行间距. 单位PX
    - % 基于当前字体尺寸的百分比
    - 可继承