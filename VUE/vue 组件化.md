# vue 组件化
### vue 组件的定义与使用
- 一个 .vue 文件就是一个 vue 组件
- 组成（3 个部分）
	- 模板页面
	```
		<template>
        页面模板
		</template>
	```
	- JS 模块对象
	```
		<script>
			export default {
				data() {return {}},
				methods: {},
          		components: {}
        	}
		</script>
	```
	- 样式
	```
		<style scoped>  //scoped代表样式只针对当前组件的模板页面
			样式定义
		</style>
	```

### 基本使用
```
	在父组件中配置子组件标签
    <template>
      <hello>
    </template>
    <script>
      import Hello from './components/Hello'
      export default {
        components: {
          Hello
        }
      }
    </script>
```

### 关于标签名与标签属性名书写的问题
- 标签名与标签属性名不区分大小写
- 标签名 -- 如果组件名是XxxYyy, 标签名必须为<xxx-yyy>
- 属性名 -- 如果标签属性名为 xxx-yyy, 组件得到的属性名为 xxxYyy

### 组件化编码的基本流程
- 拆分界面，抽取组件
- 编写静态组件并使用
- 编写动态组件并使用
	- 初始化数据，动态显示初始化界面
	- 实现与用户交互的功能

### 组件间通信
#### 组件间通信的两种方式
- props
- vue 的自定义事件
- vuex

#### 基本原则
- 不要在子组件中直接修改父组件的状态数据

#### 使用 props
- 组件标签 -- `<my-component name='tom' :age='myAge' :set-name='setName'></my-component>`

#### 组件 -- Mycomponent
- 在组件内部声明所有的 props
```
	//方式一: 只指定名称
	props: ['name', 'age', 'setName']
	//方式二: 指定名称和类型
	props: {
		name: String,
		age: Number,
		setNmae: Function
	}
	//方式三: 指定名称/类型/必要性/默认值
	props: {
		name: {type: String, required: true, default:xxx},
	}
```
- 所有 props 的属性都会成为 component 对象的属性，模板页面可以直接引用

#### 使用 vue 的自定义事件机制
- 绑定事件监听
```
	// 方式一: 通过v-on绑定
	@delete_todo="deleteTodo"
	// 方式二: 通过$on()
	this.$refs.xxx.$on('delete_todo', function (todo) {
	  this.deleteTodo(todo)
	})
```
- 触发事件
`this.$emit(eventName, data): 触发事件(只能在父组件中接收)`