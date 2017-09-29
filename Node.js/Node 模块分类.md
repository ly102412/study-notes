# Node 模块分类
### 原生模块（核心模块）
- Node.js 标准 API 中提供的模块即为核心模块，诸如：js/http/net 等
- 用法 -- var http = require('http');
- require 的参数名就是模块名

### 文件模块（非官方编写）
- 用法
	- 模块 -- var http = require('/myDir/myModule.js');
	- 包 -- var http = require('/myDir/myPackage');
- reauire 的参数是明确的路径

> 注意
> 网络下载的包不明确路径时 require 会从当前目录下开始寻找，如果找不到就会继续向上级目录寻找，直到找到根目录，如果还没有就会报错（建议目录越短越好，节省磁盘空间）
> 包中的 json 文件中需要先配置一个入口，决定先用那个文件 -- 'mian':'xxx.js'