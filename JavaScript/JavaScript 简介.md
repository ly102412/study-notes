# JavaScript 简介
### 概念
- JavaScript 被称为解释型脚本语言，简称 JS

### 兼容性问题
- 其他浏览器 -- JavaScript
- IE 浏览器 
	- IE6/7/8 -- JScript
	- IE9/10/11/Edge -- 兼容性越来越好

### JavaScript 的组成部分
- EMCAScript（脚本语言的语法）+ DOM（文档对象模型（Docment Object Model））+ BOM（浏览器对象模型（Browser Object Model））
- ECMAScript（脚本语言的语法） -- 所谓的语法，其实就是这门语言的规则，它包括名称规则、变量、函数、语法等
- DOM（文档对象模型（Document Object Model）） -- 主要用于 JavaScript 与 HTML 页面之间的交互
- BOM（浏览器对象模型（Browser Object Model）） -- 主要为浏览器提供一系列的对象内容

### EMCAScript 的版本
- 目前所学的版本 -- EMCA5
- 后面课程学习的版本 -- EMCA6/2015
- 目前最新的版本 -- EMCA7/2016
- 即将推出的版本 -- EMCA8/2017

### JavaScript 的使用
- 客户端 JavaScript（HTML 页面）
	- 第一种方式
		- 在HTML页面中编写JavaScript
        - 编写在<script></script>标签内
        - 属性
	        - type属性--设置当前脚本语言的类型--JavaScript-text/javascript（注：HTML5版本允许不设置type属性）
            - language属性--设置当前使用的脚本语言 -- JavaScript（注：该属性是一个旧的属性目前已被废弃）
            - 设定的规则--统一写在 `<body>` 便签的后边（注：其实可以写在 HTML 页面中的任何位置，这里只是人为规定）
	- 第二种方式：编写独立的JavaScript文件
	    - 创建一个 JavaScript 文件 -- 扩展名为".js"
        - 在 HTML 页面的`<head>`标签中使用`<script>`标签引入
        - 通过 src 属性引入 JavaScript 文件
        - 设定的规则 -- 统一写在`<head>`标签中
- 服务器端 JavaScript（Node.js）
	- 需要安装 Node.js 环境