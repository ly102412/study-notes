# vuex
### vuex 是什么
- GitHub -- https://github.com/vuejs/vuex
- 文档 -- vuex.vuejs.org
- 安装 -- npm install vuex --save

### vuex 概念
- vuex 是一个专为 vue.js 应用程序开发的状态管理模式
- 它采用集中式存储管理应用的所有组件的状态，并以响应的规则保证状态以一种可预测的方式发生变化
- 简单的说就是对应用中组件的状态进行集中式的管理（读/写）

### 状态自管理应用
- state -- 驱动应用数据，相当于 data
- view -- 以声明式方式将 state 映射到视图
- actions -- 相应在 view 上的用户输入导致的状态变化（包含 n 个更新状态的方法）

![单向数据流](https://vuex.vuejs.org/zh-cn/images/flow.png)

### 多组件共享状态的问题（单项数据流的间接性很容易被破坏）
- 多个视图依赖于同一状态
- 来自不同视图的行为需要变更同一状态
- 以前的解决方法
	- 将数据以及操作数据的行为都定义在父组件
	- 将数据以及操作数据的行为传递给需要的各个子组件（有可能需要多级传递）

![vuex结构](https://vuex.vuejs.org/zh-cn/images/vuex.png)

### vuex 的核心概念
#### state
- vuex 管理的状态对象
- 单一状态树（唯一数据源），用一个对象就包含了全部的应用层级状态
- 每个应用将仅仅包含一个 store 实例
- 单一状态树让我们能够直接的定位任一特定的状态片段，在调试过程中也能轻易地取得整个当前应用状态的快照
- vuex 通过 store 选项，提供了一种机制将状态从根组件“注入”到每一个子组件中（需调用 Vue.use(Vuex)）
- 通过在根实例中注册 store 选项，该 store 实例会注入到根组件下的所有子组件中，且子组件能通过 this.$store 访问到
- 代码
	```
		const state = {
			xxx: initValue
		}
	```

#### Mutations
- 包含多个更新 state 的方法（回调函数）的对象
- 由 action 中的 commit 方法来触发
- 只能包含同步的代码，不能写异步代码
- 代码
	```
		const mutations = {
			yyy(state,data){
				// 更新 state 的某个属性
			}
		}
	```

#### actions
- 包含多个事件回调函数的对象
- 通过执行 commit() 来触发 mutation 的调用，间接更新 state
- 由组件中的 $state.dispatch('action 名称') 触发
- 可包含多个异步操作
	- 定时器
	- ajax
- 代码
	```
		const actions = {
			zzz({commit,state},data){
				commit('yyy') // 事件名
			}
		}
	```

#### Getters
- 包含多个计算属性（get）对象
- 由 $store.getters.xxx 来读取
- store 中定义 Getters（可以认为是 store 的计算属性）
- 代码
	```
		const getters = {
			mmm (state) {
				return
			}
		}
	```

#### Modules
- 包含多个 module
- 一个 module 是一个 store 的配置对象
- 与一个组件（包含有共享数据）对应

#### 向外暴露 store 对象
```
	export default new Vuex.store({
		state,
		mutations,
		actions,
		getters
	})
```

#### 在组件中映射
```
	import {mapGetters,mapActions} from 'vuex';
	export default ({
		computed: mapGetters(['mmm']);
		methods: mapActions(['zzz']);
	});

	{{mmm}} @click='zzz(data)';
```

#### 映射 store
```
	import store from './store';
	new Vue ({
		store
	})
```

#### 将 vuex 引到项目中
- 下载 -- npm install vuex --save
- 使用 vuex
	- store.js
		```
			import Vuex from 'vuex';
			export default new Vuex.Store({
				state,
				mutations,
				actions,
				getters,
				modules
			})
		```
	- main.js
		```
			import store from './store.js';
			new Vue ({
				store
			}) 
		```
![](http://i.imgur.com/oL4GZt7.png)


