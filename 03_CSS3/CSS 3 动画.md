# CSS 3 动画

### 定义
- 使元素从一种样式逐渐变化到另外一种样式

### 原理
- 视觉暂留：人类具有“ 视觉暂留 ”的特征，人的眼睛在看到一幅画或一个物体后 0.34s 内不会消失
- 动画原理：通过把人物的表情、动作等的变化分解成许多动作瞬间的画幅，利用视觉暂留原理，在一幅画还没消失前播放下一幅画面，就会给人造成一种流畅的视觉变化果

### 语法
- 定义
	- keyframes是指关键帧的意思，用来决定动画发生变化的位置（注：keyframes 控制的是关键位置而不是全部位置）
- 语法
	```
		keyframes animationname{
        	keyframes-selector{
            	cssStyles；
            }
        }
	```
- 参数说明
	- animationname：必填项，定义动画的名称
    - keyframes-selector：必填项，表示动画持续时间的百分比（注：0% ~ 100% 之间或者使用 form 和to关键字也可以设置，form 代表 0%，to 代表 100%）

### animation 属性
- animation-name 属性
	- 定义 -- 设置对象的动画名称
    - 语法 -- animation-name：keyframename | none
    - 参数说明 -- keyframename：指定绑定到的选择器的关键帧的名称
- animation-duration 属性
    - 定义 -- 设置动画的持续时间
    - 语法 -- animation -duration：time
    - 参数说明 -- 设置动画播放完成所花费的时间，默认值为 0
- animation-timing-function 属性
    - 定义 -- 设置动画的过渡类型
    - 语法 -- animation-timing-function：ease
    - 参数说明
	    - linear：线性过渡（匀速）
        - ease：平滑过渡（0 - 慢 - 快 - 慢），默认值
        - ease-in：慢 - 快
        - ease-out：快 - 慢
        - ease-in-out：慢 - 快 - 慢
        - 贝塞尔曲线
- animation-delay 属性
	- 定义 -- 设置动画延迟多长时间后播放
    - 语法 -- animation-delay：time
    - 参数说明 -- 可选值，定义动画延迟多久后播放，以秒或毫秒为单位
- animation-iteration-count 属性
    - 定义 -- 设置动画的循环次数
    - 语法 -- animation-iteration-count：infinite | number
    - 参数说明
		- number：设置循环次数，为数字值，默认值是 1
        - infinite：无限循环
- animation-direction 属性
    - 定义 -- 设置动画是否反向运动
    - 语法 -- animation-direction：normal | reserve | alternate | alternate-reserve
    - 参数说明
	    - normal：正常方向（如旋转的参数设为正值则顺时针旋转）
        - reserve：反向运动
        - alternate：先正常运动再反向运动，并持续交替进行（注：需要配合循环属性使用）
        - alternate-reserve：先反向运动再正向运动，并持续交替进行（注：需要配合循环属性使用）
- animation-play-state 属性
    - 定义 -- 设置动画是否正在运行或已经处于停止状态
    - 语法 -- animation-play-state：paused | running
    - 参数说明
	    - paused：动画暂停
        - running：默认值，动画正在运行

- animation 复合属性
    - 定义 -- 设置对象所应用的动画效果
    - 语法 -- animation：name duration timing-function delay interation-count direction play-state