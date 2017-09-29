# React Ajax
### 集成 axios
- npm 下载
	`npm install axios --save`
- BootCDN 引入
	`https://cdn.bootcss.com/axios/0.16.1/axios.js`
- GitHub 上的 axios
	`https://github.com/mzabriskie/axios` 
- 实例代码
	- GET 请求
		```
			axios.get('/user?ID=12345')
			  .then(function (response) {
				console.log(response);
			})
			  .catch(function (error) {
				console.log(error);
			  });
		```
	- POST 请求
		```
			axios.post('/user', {
				firstName: 'Fred',
				lastName: 'Flintstone'
			})
			  .then(function (response) {
				console.log(response);
			  })
			  .catch(function (error) {
				console.log(error);
			  });
		```

### 集成 fetch
- BootCDN 引入
	`https://cdn.bootcss.com/fetch/2.0.1/fetch.min.js`
- fetch 文章
	`https://segmentfault.com/a/1190000003810652`
- 实例代码
	```
		fetch(url).then(function(response) {
		  return response.json();
		}).then(function(data) {
		  console.log(data);
		}).catch(function(e) {
		  console.log("Oops, error");
		});

		//ES6 箭头函数
		fetch(url).then(response => response.json())
		  .then(data => console.log(data))
		  .catch(e => console.log("Oops, error", e))
	```
