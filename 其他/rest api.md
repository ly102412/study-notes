# rest api
### 理解 rest api
#### api 接口的分类
- restful -- rest 风格
- restless -- 非 rest 风格

#### rest 接口
- https://api.github.com/users/zxfjd3g
- https://api.github.com/users/zxfjd3g/repos
- 不用带行为参数，参数是路径的一个节点
- 请求的行为由请求方式来决定
	- get -- 查询（读、获取数据） -- R -- read
	- post -- 添加（保存） -- C -- create
	- delete -- 删除 -- D -- delete
	- put -- 更新 -- U -- update

#### 非 rest 接口
- http://xxx.com/api/getUser
- http://newsapi.gugujiankong.com/Handler.ashx?action=login&username=zxfjd3g&password=123123
- 路径或参数中包含了行为数据
- 一般只有 2 中请求方式
	- get
	- post

### 模拟实现 rest 接口
- 使用 json-server 库
- 使用
	- 下载 json-server
	- 创建一个数据库文件 -- src/mock/db.json
	- 启动服务器 -- json-server --watch src/mock/db.json
- 编码测试访问 rest 接口
	- axios
	- axios.get() -- get 请求，查询
	- axios.post() -- post 请求，保存
	- axios.put() -- put 请求，更新
	- axios.delete() -- delete 请求，删除