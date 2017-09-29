# vue 生命周期
### 初始化显示
- new vue()
- beforeCreate()
- created() : 在此启动异步任务(ajax请求, 定时器)
- beforeMount()
- mounted(): 在此启动异步任务(ajax请求, 定时器)

### 更新: this.xxx = value
- beforeUpdate()
- updated()

### 销毁vue实例: vm.$destory()
- beforeDestroy(): 在此做一些收尾的工作: 如清理定时器
- destroyed()

![](../img/img29.png)