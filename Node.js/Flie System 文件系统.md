# Flie System 文件系统

- 通过文件系统可以使用 Node 来对系统中的文件做各种增删改查的操作
- Node 中通过 fs 模块来操作文件系统
- 引入 fs 模块
	- var fs = require（“ fs ”）;
- fs 中的大部分方法都有两个版本，异步版本（不带 Sync）和同步版本（带 Sync）
- fs 中的方法：
	- 打开文件
	    - fs.open（path, flags[, mode], callback）
        - fs.openSync（path, flags[, mode ]）
        	- 参数：
	            - path：文件的路径，可以使用相对路径也可以使用绝对路径
                - flags：文件的操作符，“ r ” -- 只读，“ w ” -- 修改， “ a ” -- 追加
                - mode：设置文件的权限，一般不需要设置
                - callback：回调函数，操作执行完毕时会调用回调函数
	                - 回调函数的参数：
	                    - err -- 错误对象，如果出现错误则 err 会是一个对象，如果没有出错则 err 是 null（错误优先）
                        - fd -- 文件描述符，如果打开成功则会返回一个文件的描述符，在后边的操作中可以通过描述符对文件进行各种操作（注：同步方法是将文件的描述符作为返回值返回）
	- 关闭文件
	    - fs.close（fd , callback）
        - fs.close（fd）
    - 同步写入
	    - fs.writeSync（fd , string [, position [, encoding] ]）
    - 异步写入
	    - fs.write（fd , string [, position [, econding ] ] , callback）
    - 简单写入
	    - fs.writeFile（file , data [, options] , callback）    
        - fs.writeFileSync（file , data [, options ]）
    - 流式写入
        - 流式写入可以多次将数据写入到文件中，流式写入适合大文件的写入
        - 步骤：
	        - 创建一个可写流
                    var writeStream = fs.createWriteStream（path [, options]）
            - 向流中写入数据
                    writeStream.write（data）    
            - 关闭流
                    writeStream.end（）
    - 简单读取
        - fs.readFile（path [, options] , callback）
        - fs.readFileSync（path [, options]）
	        - 参数：
            	- path -- 要读取文件的路径
                - options -- 配置对象
                - callback -- 回调函数
	                - 参数：
	                    - err -- 错误对象
                        - data -- 文件中读取到的数据，它是一个 Buffer
- 流式读取 + 写入
	- 流式读取适合大文件的读取
	    - 方法一：
		    - 步骤：
	            - 创建一个可读流
                    `var readStream = fs.createReadStream（path）`
	            - 创建一个可写流
                    `var writeStream = fs.createWriteStream（path）`
	            - 读取可读流中的内容 -- 需要给可读流绑定一个 data 事件，绑定之后，流会自动将读取到的数据通过回调函数返回（注：对于大文件来说，流会分多次读取文件）
                    ```
					readStream.on（“ data” , function（data）{
                             writeStream.write（data）;
                    }）;
					```
	            - 监听流的打开和关闭事件
		            ```
                    readStream.once（” open “ , function（）{
                              console.log（” 流打开了 “）;
                    }）;
                    readStream.once（” close“ , function（）{
                              console.log（” 流关闭了 “）;
                              // 数据读取完毕时，关闭可写流
                              writeStream.end（）;
                    }）;
                    writeStream.once（” open“ , function（）{
                              console.log（” 可写流打开了“）;
                    }）;
                    writeStream.once（” close“ , function（）{
                              console.log（” 可写流关闭了“）;
                    }）;
					```
		- 方法二：
	        - 步骤：
	            - 创建一个可读流
                    `var readStream = fs.createReadStream（path）`
	            - 创建一个可写流
                    `var writeStream = fs.createWriteStream（path）`
	            - 将可读流中的内容输入到可写流中，直接调用 pipe（）方法
                    `readStream.pipe（writeStream）`
	            - 监听流的打开和关闭事件
	            	```
                    readStream.once（” open “ , function（）{
                              console.log（” 流打开了 “）;
                    }）;
                    readStream.once（” close“ , function（）{
                              console.log（” 流关闭了 “）;
                    }）;
                    writeStream.once（” open“ , function（）{
                              console.log（” 可写流打开了“）;
                    }）;
                    writeStream.once（” close“ , function（）{
                              console.log（” 可写流关闭了“）;
                    }）;
					```
- 其他文件系统方法
	- fs.existsSync（path） -- 检查一个文件是否存在，如果存在则返回 true，不存在则返回 false   
    - fs.stat（path，callback）/ fs.statSync（path）-- 获取文件的状态（其中回调函数的参数是 err 和 stats ，stats 保存了当前文件的相关信息） 
    - fs.unlink（path，callback）/ fs.unlinkSync（path） -- 删除一个文件（其中回调函数的参数是 err）
    - fs.readdir（path [, options] , callback）/ fs.readdirSync（path [, options]） -- 读取目录的内容（其中回调函数的参数是 err 和 files，files 是一个数组，保存了文件夹下所有文件的名字）
    - fs.truncate（path，len，callback）/ fs.truncateSync（path，len）-- 截断文件（参数 len 为截断的长度 回调函数的参数是 err）
    - fs.mkdir（path[, mode ] , callback）/ fs.mkdirSync（path[, mode ]）-- 创建目录（其中回调函数的参数是 err）
    - fs.rmdir（path，callback）/ fs.remdirSync（path[, mode]）-- 删除文件夹（其中回调函数的参数是 err）         
    - fs.rename（oldPath,newPath,callback）/ fs.renameSync（oldPath,newPath）-- 重命名一个文件（其中回调函数的参数是 err ，将 newPath 设为一个新的地址可以将文件剪切到这个地址）
    - fs.watchFile（filename[ , options ] , listener） -- 监视文件的修改（其中回调函数的参数是 curr 和 prev，curr 表示当前的状态（改之后），prev 表示之前的状态（改之前）） 

-----
- 官方已建议采用异步的方式
	- 异步的优点 --  后面的代码会尽早的执行，程序执行效率比较高 
	- 异步的缺点 --  程序员编程思维要求高，容易出错，调试困难。嵌套回调函数可读性低
	- 同步的优点 -- 编程简单,对程序员的思维要求比较低
	- 同步的缺点 -- 代码执行效率较低, 在大规模访问情况下, 整个系统的响应速度慢
	- 异步的特点 -- 具有事件和回调函数，只有事件发生,回调函数才执行
	- 同步的特点 -- 没有回调函数，也没有事件，完全按照行号一行一行的执行

-----
- 绝对路径 / 相对路径
	- 文件系统
		- 绝对路径 -- 根目录
		- 相对路径 -- 以当前目录为基准
	- http url 文件路径
		- 绝对路径
			- 从 http： 开始的路径
			- 从 http url 文件路径的根目录开始
		- 相对路径
			- ./ -- 表示当前目录下的文件，当前目录就是当前文件路径的最后一个目录
			- ../ -- 上一层目录
              
                    
                        