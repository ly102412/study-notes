## AJAX 高级

### 基础
- var xhr = new XMLHttpRequest()
- 设置 response 的类型
	- 属性 responseType
	- 属性值 
		- 默认值:＂＂ -- String 类型
		- "text" -- String 类型
		- "document" -- Doument 对象类型，返回xml格式使用
		- "json" -- javascript 对象类型，IE不支持
		- "blob" -- Blob 对象类型
		- "arrayBuffer" -- ArrayBuffer 对象类型
	- 实例 
		```
		//设置请求返回数据的类型为二进制类型数据
		xhr.responseType = 'blob';  
		```
- 获取 response 的数据
	- xhr.response
		- 默认值为空字符串 -- ""
		- 当请求完成时该属性才有正确的值
	- xhr.responseText
		- 默认值为空字符串 -- ""
		- 只有当 responseType 为"text"或者" "时，此属性才能被读取，否则报错
	-  xhr.responseXML
		- 默认值为 null
		- 该类型不常用
		- 只有当 responseType 为"text"或者" "或者"document"时，此属性才能被读取，否则报错
		
- 报文首部字段
	- 设置请求报文首部字段
		- xhr.setRequestHeader('content-type', 'xxx');
	- 获得响应报文首部字段
		- xhr.getResponseHeader('Content-Type:'); 
		- 可能的返回值 -- video/x-ms-wmv

### AJAX 高级事件系统
- 服务器上传数据
	- 附着在 xhr.upload 对象上
	- 七大事件
		- xhr.upload.onloadstart 
		- xhr.upload.onprogress
			- 每50ms触发一次 
			- 上传数据时触发
			- xhr.send()之后 xhr.readystate=2之前
			- 此时 xhr.readyState == 1
		- xhr.upload.onabort -- 清除
		- xhr.upload.timeout -- 超时
		- xhr.upload.error -- 出错
		- xhr.upload.load -- 完成 
			- 上传完成,完全上传完数据时触发,此时xhr.readyState == 1
		- xhr.upload.onloadend -- 结束

- 从服务器下载
	- 附着在 xhr 对象本身上
	- 七大事件
		- xhr.onloadstart -- 调用send()后触发,此时readyState == 1
		- xhr.onprogress 
			- 每 50ms 触发一次 
			- 下载数据但未完成时触发
			- xhr.send() -- readystate == 3 之后 readystate == 4之前
			- 此时 xhr.readyState == 3
		- xhr.onabort -- 清除
		- xhr.timeout -- 超时
		- xhr.error -- 出错
		- xhr.load -- 完成
			- 下载完成,完全获得服务器数据时触发,此时readyState == 4
		- xhr.onloadend -- 结束

- readyState 的切换事件
	- 附着在 xhr 对象上
	- onreadystatechange 
	- readystate状态改变时执行. 总共执行四次
	
- 事件的触发顺序

![](http://i.imgur.com/BM0WVHw.png)

