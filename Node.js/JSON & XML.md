# JSON & XML
### JSON
- 全称 JavaScript Object Notation
- 译为 JavaScript 对象标记
- 具有特定格式的字符串
- 对应的一种文件 -- xxx.json

### XML 
- 全称 Extensive Markup Language
- 译为可扩展标记语言
- 对应的一种文件 -- xxx.xml

### JSON 与 XML 的相同点 
- 都具有层级结构，保存结构化数据
- 可以通过 JavaScript 解析
- 数据可通过 AJAX 进行传输
- 纯文本，独立于特定的语言
- 可在网络上传输（客户端发送到服务器，服务器返回客户端）
- 可做配置文件
- 具有“自我描述性”（人类可读）

### JSON 优势
- 体积更小
- 节省带宽
- JS 操作更方便

------
### JSON 详解
- 名值对必须是双引号的字符串
- 不允许有注释
- JSON 类型
	- key 类型是字符串，value 可以是 num，str，bool，null，{}，[]
	- 对象 -- {key1:value1,key2:value2}
	- 数组 -- [value1，value2]
- JSON 工具对象
	- object parse(json) -- json 字符串转 obj 对象
		`var obj = JSON.parse(str);`
	- string stringify(object) -- obj 对象转成 json 字符串
		`var srt = JSON.stringify(obj)`
- JSON 字符串与 JS 对象
	- 区别
		- JSON 是符合某种规范格式的字符串
		- JS 对象是堆空间中的一段内存
	- 联系
		- 存储的信息相同
		- 规范很像
		- 非常容易相互转化