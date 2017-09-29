# jQuery 入门
### JavaScript 类库
- 作用 -- JavaScript 类库的出现，就是为了简化 JavaScript 的开发
- 内容 -- JavaScript 类库封装了预定义的对象和函数
- 目的 -- 帮助开发人员建立有高难度交互的 Web2.0 特性的富客户端页面，并且兼容各大浏览器
- 扩展内容
	- Web2.0 相关概念
		- Web1.0 -- 网络 -> 人（单向信息。网络是信息的提供者，单向的提供和单一理解）
		- Web2.0 -- 人 -> 人（以网络为沟通渠道进行人与人的沟通。网络是平台，用户提供信息，通过网络其他用户获取信息）
		- Web3.0 -- 人 -> 网络 -> 人（人与网络之间的双向沟通。网络成为用户需求理解者和提供者）
	- 富客户端与瘦客户端
		- 富客户端（Rich Internet Applications，RIA） -- 利用具有很强交互性的富客户端技术为用户提供一个更高和更全方位的网络体验
		- 瘦客户端（Thin Client）-- 指的是在客户端-服务器网络体系中的一个基本无需应用程序的计算机终端 

### jQuery 的简介
- jQuery 的两个文件 
	- 正常版本 -- 用于学习和研究使用
	- 压缩版本 -- 用于正式生产环境
- jQuery 目前的版本
    - 1.x版本 -- 几乎兼容所有的浏览器
    - 2.x版本 -- 不在兼容 IE 所有的浏览器
    - 3.x版本 -- 不在兼容 IE8 之前的版本         
- jQuery 的四个模块
	- jQuery -- 针对 PC 端浏览器
    - jQuery UI -- 针对样式
    - jQuery Mobile -- 针对移动端浏览器
    - Qunit -- 针对前段测试 

### jQuery 编程的步骤
- 在 HTML 页面引入 jQuery 文件
	```
		<!-- 1\. 引入jQuery文件 -->
		<script src="jquery-1.11.3.js"></script>
	```
- 在 HTML 页面中定义元素
	```
		<!-- 定义HTML页面元素 -->
		<input type="text" value="请输入你的用户名" id="username">
	```
- 使用 jQuery 的选择器定位元素
	```
		// 2. 使用jQuery选择器定位HTML页面元素
		var $username = $("#username");
	```
- 利用 jQuery 提供的 API 完成需求
	```
		// 3. 调用jQuery的API方法
		console.log($username.val());
	```