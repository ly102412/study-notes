# vue-router
### 说明
- 官方提供的用来实现 SPA 的 vue 插件
- github: https://github.com/vuejs/vue-router
- 中文文档: http://router.vuejs.org/zh-cn/
- 下载: npm install vue-router --save

### 相关 API 说明
#### VueRouter()
- 用于创建路由器的构建函数
- 代码
```
	new VueRouter({
      // 多个配置项
    })
```

#### 配置路由
- 代码
```
	routes: [
		{ // 一般路由
			path: '/about',
			component: about
		},
		{ // 自动跳转路由
			path: '/', 
			redirect: '/about'
		}
	]
```

#### 组件
- router-link
	- 用来生成路由链接
	- `<router-link to="/xxx">Go to XXX</router-link>`
- <router-view>
	- 用来显示当前路由组件界面
	- `<router-view></router-view>`

### 实现简单路由
#### 路由组件
```
	home.vue
	about.vue
```
#### 应用组件 -- App.vue
```
	<div>
      <!--路由链接-->
      <router-link to="/about">About</router-link>
      <router-link to="/home">Home</router-link>
      <!--用于渲染当前路由组件-->
      <router-view></router-view>  
    </div>
```
#### 入口 JS -- main.js
```
	// 创建路由器(配置路由)
    new VueRouter({
      routes: [
        {
          path: '/',
          redirect: '/about'
        },
        {
          path: '/about',
          component: about
        },
        {
          path: '/home',
          component: home
        }
      ]
    })
      
    // 创建vue配置路由器
    new Vue({
      el: '#app',
      router,
      render: h => h(app)
    })
```
#### 优化路由器配置
```
	linkActiveClass: 'active', // 指定选中的路由链接的class
    mode: 'history',  // 路由路径不带#
```

### 嵌套路由
#### 配置嵌套路由
```
	path: '/home',
    component: home,
    children: [
      {
        path: 'news',
        component: news
      },
      {
        path: 'message',
        component: message
      }
    ]
```
#### 路由路径
```
	<router-link to="/home/news">News</router-link>
    <router-link to="/home/message">Message</router-link>
```

### 向路由组件传递数据
#### 路由路径携带参数
- 配置路由
	```
		children: [
			{
				path: 'mdetail/:id',
				component: messageDetail
			}
		]
	```
- 路由路径
	`<router-link :to="'/home/message/mdetail/'+m.id">{{m.title}}</router-link>`
- 路由组件中读取请求参数
	`this.$route.params.id`

#### `<router-view>`属性携带数据
`<router-view :msg="msg"></router-view>`

### 其他重要
#### 使用`<keep-alive>`缓存路由组件
```
	<keep-alive>
      <router-view></router-view>
    </keep-alive>
``` 

#### 路由组件中监视路由参数的变化
```
	watch: {
      '$route' (to, from) {
        // to为包含最新参数的$route对象
      }
    }
```
