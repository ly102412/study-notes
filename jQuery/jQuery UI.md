# jQuery UI
### jQuery UI 的简介
- jQuery UI 能做的事可谓是包罗万象，实际上，jQuery UI 在某种意义上并不是插件，而是一个完整的插件库
- jQuery UI 中主要包含以下几个功能
	- Effect（效果）
	- Interactions（交互组件）
	- Widget（部件）
	- 此外，还为 jQuery 和核心动画提供了很多高级效果

### 使用方法
-  引入ui -- jquery-ui.js
-  引入themes -- base -- jquery-ui.css / imagse(同级目录)
-  引入demos -- demos.css

### Effects -- 动画效果
- animate（）-- 扩展 jQuery 中的 animate（） 方法
	- 允许改变有关颜色的 CSS 样式内容
    - 注：设置颜色的格式时不能使用单词形式定义颜色内容
- effect（effect，options，duration，callback）
   - effect -- 表示设置的动画效果
     blind
     bounce
   - options -- 选项
   - duration -- 表示动画执行的时长，单位为毫秒
   - callback -- 表示动画执行完毕后的回调函数
- Widgets -- HTML 组件
	- 折叠面板
    - 提示框
    - 日期控件
    - 页签
- Interactions -- 操作