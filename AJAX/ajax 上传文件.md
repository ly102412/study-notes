## ajax 上传文件
### BUG 调试
- 开发者工具控制台
- 阅读错误信息，找到对应的代码的行号
- 打断点，重新运行
- 观察变量是否正确获取到值
- 如果变量无误检查服务器发来的数据
- 用浏览器发送服务器的请求进行测试能否收到结果

### multer 上传文件包
- 处理浏览器上传的文件，运行高效
- 安装 -- $ npm install --save multer
- 路由文件中引入 -- var multer  = require('multer')

### 单文件上传
#### 服务器端工作
- 搭建上传文件环境，引入 multer 和 path 包
- 设置磁盘写入路径
	- 生成磁盘配置对象
	- 生成上传中间件
	- 设定文件存储位置
	- 设置 storage 配置对象
		- 设置磁盘文件夹信息（函数）
		- 设置磁盘文件信息（函数）

> 注
>	- req.file 所包含的信息
		- 浏览器信息
			- fieldname 在 form 中 input 标签的 name 属性
			- originalname 在用户电脑中文件的名字
		- 磁盘存储信息
			- destination 服务器端 目录名
			- filename 服务器端 文件名
			- path 服务器端完全路径 
>	- router 路由写法（重要!! 可以直接复制粘贴使用）
			var router = require('express').Router();
			//引入 path包
			var path = require('path');
			//引入 multer 上传文件的包
			var multer = require('multer');
			//设置磁盘写入路径和文件名规范
			//1.生成磁盘配置对象
			var distStorage = multer.diskStorage({
			  destination: setDirectoryInfo,    //设置磁盘文件夹信息 函数
			  filename: setFileInfo             //设置文件相关信息 函数
			});
			//2.接收文件的目录
			var upload = multer({storage: distStorage});
			//3.设定文件存储的位置，需要提前建立好文件夹
			var DIRECTORY_PATH = '../public/upload_files';
			//4-1.设置磁盘文件夹信息
			function setDirectoryInfo(req, file, cb) {
			  //回调函数的固定写法
			  cb(null, DIRECTORY_PATH);   //错误优先
			}
			//4-2.设置文件相关信息
			function setFileInfo(req, file, cb) {
			// 浏览器上传时候的 input 标签 name 值
			  var fileName = file.fieldname;  
			//重要!! 打上时间戳并且提供随机数保证文件名不会重复，否则会覆盖.
			  fileName += '_' + Date.now() + '_'+ Math.floor(Math.random() * 1000);   
			  var originalName = file.originalname;             //获得用户上传文件的原名
			  var extensionName = path.extname(originalName);   //获得扩展名. 需要提前引入path包
			  fileName += extensionName;      //拼接扩展名
			  cb(null, fileName);             //回调函数的固定写法
			}

>	- 简单写法备注 -- var upload = multer( dest: 接收上传文件路径})

- post 发送请求
	- 第一个参数 -- form 表单 action 的路由
	- 第二个参数 -- 接收文件的目录并调用 single 函数
		- single 函数内写入 input 上传文件标签中 name 的值
	- 第三个参 -- 回调函数，上传后执行
	- 实例
		```
			router.post('/uploadSingleFile',upload.single('avatar'),function (req,res,next) {
	  			res.send('单文件上传成功')
			});
		```

#### 客户端工作
##### 原生 from 表单上
- from表单必须要设置的
	- action -- 服务器路由
	- method -- post 
	- enctype -- 编码格式 "multipart/form-data"
- input标签属性
	- type="file" -- 上传文件按钮
	- name 的值是需要传入 single 函数里的
- 优点 -- 实现简单
- 缺点 -- 会刷新整个页面
- 实例
	```
		<form action="/uploadSingleFile" method="post" enctype="multipart/form-data">
	        <input type="file" name="avatar">
	        <input type="text" name="username" value="">
	        <input type="submit" value="上传">
    	</form>
	```

##### ajax 异步上传单文件
- from 表单必须要设置的
	- id -- 表单的唯一标识
	- method -- post 
	- enctyp -- 编码格式 "multipart/form-data"
	- 引入 ajax 的 js 文件
- ajax文件
	- 正常创建 ajax 对象 xmlHttpRequest
	- FormData对象
		- 表单数据序列化(一串一串地数据) 将表单数据传输到服务器
		- 获得页面中 form 表单的 id
		- 实例化 FormData 
		`var myFormData = new FormData(formID);`
		- 发送实例 FormData (不用设置请求头)
		`send(myFormData);`

- 优点 -- 不需要刷新页面，使用方便
- 缺点 -- 兼容性问题 IE10以下不可用
- 实例
	```
		<form id="formId" method="POST" enctype="multipart/form-data" >
	    	<span>上传头像:</span> <input type="file" name="avatar">
	    	<br>
		</form>
		<input type="button" id="submit" name="submit" value="上传"/>

		ajax js文件:
		//找到上传按钮
		var submit = document.getElementById('submit');
		
		//点击提交按钮
		submit.onclick = function(){
		console.log('提交按钮被点击');
		
	    //1.创建 xhr 对象
	    var xhr = new XMLHttpRequest();
	
	    //2.创建 FormData 对象  重要!!!
	    //2-1.获得页面中form表单的id
	      var formEle = document.getElementById('formId');
	    //2-2.实例化 formData
	      var data = new FormData(formEle);
	
	    //3.设置回调函数
	    xhr.onreadystatechange = function () {
	    	  if(xhr.readyState === 4 && xhr.status ===200){
	    	      var result = xhr.responseText;
	    	      console.log(result);
	        }
	    };

	    //open 函数设置参数
	    xhr.open('POST','/uploadSingleFile');
	
	    //发送数据FormData对象  注意：使用了FormData就不用设置请求头
	    xhr.send(data);
		};	
	```

##### form + iframe 上传单文件(了解即可)
- 流程:
	- 动态创建 form 和 iframe 元素
	- 把 form 装到 iframe 里面，这样刷新的是 iframe 而不是当前页面
	- 给页面的 input 标签，添加一个 change 事件监听
	- 当用户选择文件的时候，自动提交 form 表单(不需要点击上传按钮)
- 优点 -- 兼容性好，克服了刷新页面问题，模拟了异步上传文件
- 缺点 -- 太过复杂

##### 图例
![](http://i.imgur.com/jBzbsU6.png)
![](http://i.imgur.com/xyvWvec.png)
![](http://i.imgur.com/NOmLLUC.png)

##### ajax 进度条
- 进度条事件体系
	- 附着在 xhr.upload 上
	- loadstart 接收到第一个字节时触发
	- progress 在上传数据期间每 50ms 触发
	- error 出错时触发
	- about 在 about 调用放弃时触发
	- load 接收到完整数据，ajax 结束时触发
	- upload 上传时触发，每 50ms 执行一次 
- 进度条重要事件
	- load 可以代替 readystatechange 事件
	- progress 
		- xhr.upload.progress = function(event){}
		- 回调函数参数 event 对象
			- event.lengthComputable 进度信息是否可用
			- event.loaded 已经下载的字节
			- event.total 总共需要下载的字节
			- 计算百分比 
		 		`var rate = Math.floor((loaded/totle) * 100) + '%'`
- progress 进度条 html 标签
`<progress id="progressId" value="" max=""></progress>`
- progress 标签属性
	- max 总共的量
	- value 正在进行当前的量
- 注意: IE10 及以下浏览器不支持该标签

#### ajax 异步结合进度条上传单文件
- from 表单必须要设置的
	- id -- 表单的唯一标识
	- method -- post 
	- enctype -- 编码格式 "multipart/form-data"
	- 引入 ajax 的 js 文件
- ajax文件
	- 正常创建 ajax 对象 xmlHttpRequest
	- FormData 对象
		- 表单数据序列化，将表单数据传输到服务器
		- 获得页面中 form 表单的 id
		- 实例化 FormData 
		`var myFormData = new FormData(myForm);`
		- 发送实例 FormData (不用设置请求头)
		`send(myFormData);`
	- 设置上传进度回调函数
		- 上传结束事件 整个 ajax 结束服务器返回消息 
			- xhr.onload
        - 上传进度事件，正在上传的时执行
	        - xhr.upload.onprogress
	
- 缺点 -- 兼容性，IE10及以下不支持   
    
- 优点
	- 真实的异步提交数据. 
	- 使用方便
	- 可以显示进度条
- 实例
	```
		/* ------------ html代码 ------------------------*/

		<body>
		<form id="formId" method="POST" enctype="multipart/form-data" >
		    <span>上传头像:</span> <input type="file" name="avatar">
		    <br>
		</form>
		<br>
		<input type="button" id="submit" name="submit" value="上传按钮"/>
		<br>
		
		<progress id="progressId" value="" max=""></progress>
		<span id="spanId"></span>
		
		</body>
	
		/*---------------- AJAX 代码 ----------------------- */
	
		//找到上传按钮
		var submit = document.getElementById('submit');
		//获取到进度条
		var progressBar = document.getElementById('progressId');
		//获取页面接收服务器返回消息的span标签
		var spanEle = document.getElementById('spanId');
		
		//点击提交按钮时
		submit.onclick = function(){
		  console.log('提交按钮被点击');
		
		  //1.创建 xhr 对象
		  var xhr = new XMLHttpRequest();
		
		  //2.创建 FormData 对象
		  //2-1.获得页面中form表单的id
		  var formEle = document.getElementById('formId');
		  //2-2.实例化 formData
		  var data = new FormData(formEle);
		
		  //3.ajax结束时从服务器返回消息执行回调函数
		  xhr.onload = function () {
		    var result = xhr.responseText;
		    console.log('result:',result);
		    //动态页面显示服务器返回的消息
		    spanEle.innerHTML = result;
		  };
		
		  //4.上传进度事件时执行回调函数
		  xhr.upload.onprogress = function (e) {
		    //onprogress 执行时机: 正在上传的时候.
		    //每50ms执行一次
		    if(e.lengthComputable){  //1. 判断进度信息是否可用
		
		      var loaded = e.loaded;  //2. 获得已经上传的数量
		      var totle = e.total; //3. 获得总共将要上传的数量  字节
		      var rate = Math.floor((loaded/totle) * 100) + '%';  //4. 取百分比
		      console.log(rate);
		
		      progressBar.value = loaded;
		      progressBar.max = totle;
		
		    }
		  };
		
		  //open 函数设置参数
		  xhr.open('POST','/uploadSingleFile');
		  
		  //发送数据FormData对象  注意：使用了FormData就不用设置请求头
		  xhr.send(data);
		};
	```

### 多文件上传
#### 服务器工作
- 发送POST请求
	- 第一个参数 -- form 表单 action 的路由
	- 第二个参数 -- 接收文件的目录并调用 fields 函数.
		- fields 函数需要一个数组
		- 数组定义了 -- 1、input标签的name的值 2、最大支持文件同名数量
	- 第三个参数 -- 回调函数，上传后执行

- 实例
	```
		var arr = [{name:'avatar',maxcount:3}];
		router.post('/uploadMultiFile',upload.fields(arr),function (req,res,next) {
			res.send('多文件上传成功')
		});
	```

#### 客户端工作

##### 原生 form 表单上传多文件
- from 表单必须要设置的
	- id -- 表单的唯一标识
	- method -- post 
	- enctype -- 编码格式 "multipart/form-data"
- input 标签
	- type="file"
	- 可以多个 input 标签 
	- 也可以设置 multiple="multiple" 提供一个 input 标签即可
	- name 可以重复,值是需要传入 fields 函数里的	
- 优点 -- 实现简单
- 缺点 -- 会刷新整个页面,无法观察进度条	
- 实例
	```
		<body>
		<form id="myForm" action="/uploadMultiFile" method="post" enctype="multipart/form-data">
		
		    <input type="file" name="avatar" multiple="multiple"> <br>
		
		    <input id="submitButton" type="submit" value="提交"> <br>
		</form>
		</body>
	```

##### AJAX异步多表单多文件上传
- from表单必须要设置的
	- id -- 表单的唯一标识
	- method -- post 
	- enctype -- 编码格式 "multipart/form-data"
	- input 标签 name 对应路由 fields 函数需要的值
	- 引入 ajax 的 js 文件
- ajax文件
	- 正常创建 ajax 对象 xmlHttpRequest
	- FormData对象
		- 表单数据序列化，将表单数据传输到服务器
		- 获得页面中 form 表单的 id
		- 实例化 FormData 
		`var myFormData = new FormData(myForm);`
		- 发送实例 FormData (不用设置请求头)
		`send(myFormData);`
	- 设置上传进度回调函数
		- 上传结束事件，整个 ajax 结束服务器返回消息 
			- xhr.onload
        - 上传进度事件，正在上传的时执行
	        - xhr.upload.onprogress
- 实例
	```
	/* ------------ html代码  ------------------------*/
	<body>
	<form id="myForm1" action="/uploadMultiFile" method="post" enctype="multipart/form-data">
		<input type="file" name="avatar" multiple="multiple"> <br>
	</form>
	<progress id="progressId1" value="" max=""></progress>
	
	<br>
	<br>
	
	<form id="myForm2" action="/uploadMultiFile" method="post" enctype="multipart/form-data">
	    <input type="file" name="photo">
	</form>
	<progress id="progressId2" value="" max=""></progress>
	
	<br>
	<br>
	
	<form id="myForm3" action="/uploadMultiFile" method="post" enctype="multipart/form-data">
	    <input type="file" name="picture">
	</form>
	<progress id="progressId3" value="" max=""></progress>
	
	<br>
	<br>
	<input id="submitButton" type="button" value="提交"> <br>
	</body>
	
	/* --------------- 路由设置 ----------------------*/
	var arr = [{name:'avatar',maxcount:1},{name:'photo',maxcount:1},{name:'picture',maxcount:1}];
	router.post('/uploadMultiFile',upload.fields(arr),function (req,res,next) {
	  res.send('多文件上传成功')
	});

	/*---------------- AJAX 代码 ----------------------- */
	var submit = document.getElementById('submitButton');
		var form1ID = 'myForm1';
		var form2ID = 'myForm2';
		var form3ID = 'myForm3';
		
		var progressId1 = 'progressId1';
		var progressId2 = 'progressId2';
		var progressId3 = 'progressId3';
	
	//当按钮点击时
	submit.onclick = function(){
	    console.log('准备上传');
	  upload(form1ID,progressId1);
	  upload(form2ID,progressId2);
	  upload(form3ID,progressId3);
	};
	
	function upload( formID,  progressId) {
	
	  //1.创建 xhr 对象
	  var xhr = new XMLHttpRequest();
	
	  //2.创建 FormData 对象
	  var myForm = document.getElementById(formID);
	  var data = new FormData(myForm);
	
	  //3.注册结束事件的回调函数  整个ajax结束服务器返回消息
	  xhr.onload = function () {
	    var result = xhr.responseText;
	    console.log('result:',result);
	  };
	
	  //4.注册上传进度事件的回调函数
	  xhr.upload.onprogress = function (e) {
	    //onprogress 执行时机: 正在上传的时候.
	    //每50ms执行一次
	    if(e.lengthComputable){  //1. 判断进度信息是否可用
	
	      var loaded = e.loaded;  //2. 获得已经上传的数量
	      var totle = e.total; //3. 获得总共将要上传的数量  字节
	      var rate = Math.floor((loaded/totle) * 100) + '%';  //4. 取百分比
	      console.log(rate);
	
	      var progressBar = document.getElementById(progressId);
	      progressBar.value = loaded;
	      progressBar.max = totle;
	
	    }
	  };
	
	  //open 函数设置参数
	  xhr.open('POST','/uploadMultiFile');
	
	  //发送数据FormData对象  注意：使用了FormData就不用设置请求头
	  xhr.send(data);
	}
	```

### 文件下载
#### 服务器端工作
- 下载使用 GET 请求方法即可
- path.join() 拼接路径
	- __dirname -- 当前工作目录下
	- 以逗号作为连接符进行路径字符串拼接
- res.download()
	- 参数 -- 要下载的文件路径
- 实例
	```
	router.get('/download',function (req,res,next) {
	    var dir = path.join(__dirname,'../','public','upload_files');
	    var filePath = path.join(dir,'avatar_1491980628992_177.jpg');
	    
		res.download(filePath)
	});
	```

#### 客户端工作
##### 普通下载
- 点击 a 标签发送请求下载
	- 输入下载时的路由路径即可
	- `<a href="/download">文件下载</a>`
- 点击按钮进行下载操作
	- js 创建 a 标签
		- `document.createElement('a');`
	- 设置 a 标签的属性
		- setAttribute('href','路由路径')
			- `a.setAttribute('href', url);`
		- setAttribute('用处','下载时的文件名')
			- `a.setAttribute('download', 'myFileName');`
	- 把标签添加到 dom 中
		- `appendChild(a);`
	- 模拟点击事件
		- `a.click(); `
		
##### 浏览器内存下载
- 创建内存数据
	- Blob([],{})
	- 第一个参数 -- 数组，值是字符串类型
	- 第二个参数 -- 对象，type: 'text/xxx',endings: 'native' 
	- `var myBlob = new Blob([data], {type: 'text/plain', endings: 'native' });`
- 模拟创建内存中的 url 地址
	- `var myUrl = URL.createObjectURL(myBlob);`
- 动态创建 a 标签 (下载文件依靠浏览器能力)
	
##### 使用 ajax 把服务器中的数据下载到内存
- 设置响应头类型
	- blob 为二进制类型数据
	- `xhr.responseType = 'blob';`
- 获得服务器返回的数据
	- `xhr.response;`

##### 使用ajax 显示进度 - 真实下载到本地

- 使用 ajax 把服务器中的数据下载到浏览器内存
- 在页面显示进度条
- 当进度条走到终点后下载服务器的内存文件到本地磁盘
- 实例
	```
	/* ------------ html代码  ------------------------*/
	<body>
	<input id="submitButton" type="button" value="下载">
	
	<div>
	    <progress id="progressId" value="" max=""></progress>
	</div>
	
	<div id="resultDiv" style="display: none"></div>
	</body>

	/*---------------- AJAX 代码 ----------------------- */
	
	//获取提交按钮
	var submit = document.getElementById('submitButton');
	//定义进度条id
	var processBarId = 'progressId';
	
	submit.onclick = function(){
	    console.log('准备下载');
	    download(processBarId, resultSpanId);
	};
		
	function download(processBarId, resultSpanId) {
	  //获得进度条标签
	  var processEle = document.getElementById(processBarId);
	  //创建 ajax实例
	  var xhr = new XMLHttpRequest();

	  //内存下载: 当下载进度进行时执行函数
	  //onprogress函数 每50ms执行一次
	  xhr.onprogress = function (e) {
	    if(e.lengthComputable){  //1. 判断进度信息是否可用
	
	      var loaded = e.loaded;  //2. 获得已经上传的数量
	      var totle = e.total; //3. 获得总共将要上传的数量  字节
	      var rate = Math.floor((loaded/totle) * 100) + '%';  //4. 取百分比
	     
	      processEle.value = loaded;
	      processEle.max = totle;
	    }
	  };
	  //当内存下载结束的时调用函数进行真实下载到本地
	  xhr.onload = function () {
	    var result = xhr.response; //得到blob实例
	    var myUrl = URL.createObjectURL(result); //创建 url 对象
	
	    //模拟a标签
	    var a = document.createElement('a');
	    a.setAttribute('href',myUrl);
	    a.setAttribute('download','file_____name');
	    document.getElementById('resultDiv').appendChild(a);
	    a.click();
	  };
	
	  //设置返回值类型
	  xhr.responseType = 'blob';
	  //open 函数
	  xhr.open('get','/download');
	  //send 函数
	  xhr.send();
	}
	```


#### Blob 
- JavaScript 的内置对象类型
- 含有size 和 type属性
- 使用构造函数创建 Blob
	- new Blob()
- 第一个参数 
	- 数组类型 -- 传入 blob 的数据
	- 数据可以是任意格式的值 (比如字符串)
- 第二个参数
	- 对象(包含以下两个部分)
	-  数据类型 -- type: 'text/xxx'
	-  endings: 'native'
- var Blob = new Blob(['xxx'], {type:'text/plain',endings:'native' });