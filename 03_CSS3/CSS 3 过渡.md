# CSS 3 过渡
### 定义
- 允许 css 的属性值在一定的时间内平滑过渡，例如，当鼠标点击时，鼠标滑过时以及对元素的任何改变中触发，并以平滑的方式改变 css 的属性值

### 属性
- transition-property 属性
	- 定义 -- 控制参与过渡的属性
    - 语法 -- transition-property：none | all | property
    - 注
	    - none -- 不控制任何属性
        - all -- 默认值，控制所有属性
        - property -- 控制指定的元素，如 color 等
- transition-duration 属性
    - 定义 -- 设置对象过渡的持续时间
   	- 语法 -- transition-duration：time
    - 注：规定完成过渡效果所需要花费的时间，以秒或者毫秒为单位，默认值为 0
- transition-timing-function 属性
    - 定义 -- 设置过渡动画的速度类型
    - 参数
	    - linear：线性过渡（匀速）
        - ease：平滑过渡（0 -- 慢 -- 快 -- 慢），默认值
        - ease-in：慢 - 快
        - ease-out：快 - 慢
        - ease-in-out：慢 - 快 - 慢
        - 贝塞尔曲线
    - 注：只能设置一个值
- transition-delay 属性
    - 定义 -- 设置延迟多长时间后执行过渡效果
    - 语法 -- transition-delay：time
    - 参数说明：在指定的延迟时间后执行过渡效果，默认值为 0
- transition 复合属性
    - 定义 -- 设置对象变换时的过渡
    - 语法 -- transition：property duration timing-function delay；
    - 注：时间的排列顺序不能改变

### 过渡的问题
- 变换函数的个数 顺序不一致的情况下，很有可能会使过渡失效
- 当元素首次加载没有结束的情况下，过渡是没有办法被触发的
- 过渡是没有办法检测到过渡过程中的每一帧的，所以即点即停不能使用过渡来完成（使用 Tween 算法时）