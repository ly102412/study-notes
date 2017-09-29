# Node.js 简介

### Node.js
- Node.js 简称 Node
- Node 简单来说可以使 JS 在服务器端运行，而不仅仅局限在浏览器中，我们也可以通过 JavaScript 来开发 WEB 服务器
- Node 是一个 ECMAScript 标准的实现，所有的 ECMAScript 标准中定义的内容在 Node 中都可以直接使用，但是在 Node 中不能使用 BOM 和 DOM 的对象
- Node 底层是通过 chrome 的 V8 引擎实现的
- Node 的功能已经不局限在服务器，它已经形成了一个生态环境并且建立了一个良好的开源的社区
- Node 的特点
	- 非阻塞，异步 I/O
    - 基于事件和回调函数
    - 单线程（主线程是单线程），后台（I/O 线程池）
    - 跨平台

### 模块化（Module）
- 模块化就是将一个完整的程序分割成一个一个模块的结构，以降低代码之间的耦合，方便代码的复用
- 原生的 JS 中没有模块化的机制，所以在 Node 中引入 CommonJS 规范，通过该规范在 Node 中成功的引入模块化（CommonJS 主要用于 Node 中的模块化规范，AMD、CMD 用于浏览器端的模块化规范）
- 模块化的使用
	- 模块的引用
    	- 使用 require（） 引入外部的模块
	        - 例子
	        	```
                	var fs = require(" fs ")；
                    var math = require（“ math ”）；
				```
    - 模块的定义
         - 在 Node 中一个 JS 文件就是一个模块，但是在 JS 文件中编写的代码，并不是直接写在全局中的，所以默认情况下模块中的代码对于外部都是不可见的 
         - 使其暴露可见的方法
	         - 使用 exports -- 可以将需要暴露的方法或属性设置为 exports 的属性，即可暴露这些内容
             - 使用 module,exports -- 也可以通过该属性来暴露内容，并且可以直接为 module.exports 进行赋值
    - 模块的标识
        - 模块的标识就是模块的名字
	        - 对于核心模块，可以直接使用模块的名字，如：fs express mongoose
            - 对于文件模块（自定义模块），需要通过文件的路径来引入，如：./hello

### 包（package）

- 一个模块只是一个单一的功能，将多个模块组合为一个更强大的功能便形成了包（包的规范同样也是由 CommonJS 来规定）
- 包的结构
	- bin 用于存放可执行的二进制文件的目录
    - lib 用于存放 JavaScript 代码的目录
    - doc 用于存放文档的目录
    - test 用于存放单元测试用的代码
- 包的描述文件
	- 用来描述包的功能、名字、作者、版本、依赖等内容
    - 包描述文件的名字：package.json
	    - 常见的属性：
	        - name 包名
            - version 包的版本
            - main 包的主要 JS 文件（程序的入口）
            - repository 仓库的地址（github 的地址）
            - dependencies 包的依赖

### NPM（Node Package Manager）
        
- Node 的包管理器
	- 提供了对 Node 的包的管理，相当于 360 中的软件管家，负责 Node 中包的上传、下载、搜索等功能
    - 安装 Node 时，NPM 会自动安装
- NPM 的指令：
    - npm -v -- 查看版本
    - npm search 包名 -- 搜索指定的包       
    - npm install -- 安装当前模块所需要的依赖模块
    - npm install 包名 -- 安装指定的包（默认情况下会直接将包安装到当前目录下的 node module 文件夹下）
    - npm install 包名 -save -- 在当前模块中安装指定的包，并将其添加到依赖中
    - npm install 包名 -g -- 全局安装包（将包安装在系统中，一般全局安装包在编写服务器时用的不多，全局安装的模块多是工具模块）      
    - npm init -- 初始化一个新的模块（创建一个 package.json）