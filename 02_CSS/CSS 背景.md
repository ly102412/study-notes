# CSS 背景
 
### background-color 设置元素背景色
- 默认 -- transparent，背景颜色为透明。
- 使用颜色名称设置背景颜色（比如：red）
- 使用十六进制值设置背景颜色（比如：#ff0000）
- 使用 rgb 代码设置背景颜色（比如 rgb（255,0,0）或 rgba（255,0,0,0.5））
        
### background-image 设置背景图像
- background-image：url（“img/timg.jpg”）；
        
### background-repeat 设置背景图像是否平铺
- repeat-x：背景图像在水平方向重复
- repeat-y：背景图像在垂直方向重复
- no-repeat：背景图像仅显示一次
        
### background-position 设置图像位置
- 50% 50%
- center
- 150px 50px
        
### background-attachment 设置背景图像是否固定或随着页面的其余部分滚动
- scroll 默认值，背景图像会随着页面其余部分的滚动而移动
- fixed 当页面的其余部分滚动时，背景图像不会移动
        
### background 简写
- background：颜色 背景图 是否平铺 是否随页面滚动 背景图位置