# vue 的使用
### 基本使用
- 引入 vue.js 
- 创建 vue 实例对象`new Vue({})`，指定选项（配置）对象
	- el -- 指定 DOM 标签容器的选择器
	- data -- 指定初始化状态属性数据的对象函数（返回一个对象）
- 页面中使用 vue 指令
	- 使用 v-model -- 实现双向数据绑定
	- 使用{{}} -- 显示数据

### vue 实例
- 每个 vue 应用的起步都是通过构造函数 vue 创建一个 vue 的根实例
- 一个 vue 实例其实正是一个 MVVM 模式中所描述的 ViewModel
- 实例
	```
		var vm = new Vue({
		  // 选项
		})
	```

### vue 对象的选项
- el 
	- 指定 DOM 标签容器的选择器
	- vue 就会管理对应的标签及其子标签
- data 
	- 对象或函数类型
	- 指定初始化状态属性数据的对象
	- vue 对象可以直接访问其属性
	- 页面中可以直接访问使用
	- 数据代理 -- 由 vm 对象来代理对 data 中所有属性的操作（读/写）
- methods
	- 包含多个方法的对象
	- 供页面中的事件指令来绑定回调
	- 回调函数默认有 event 属性，但也可以指定自己的参数
	- 所有的方法由 vue 对象来调用，访问 data 中的属性直接使用 this.xxx
- computed
	- 包含多个方法的对象
	- 对状态属性进行计算返回一个新的数据，供页面获取显示
	- 一般情况下相当于是一个只读属性
	- 利用 set/get 方法来实现属性数据的计算读取，同时监视属性数据的变化
	- 如何给对象定义 get/set 属性
		- 在创建对象时指定
			`get name () {return xxx} / set name (value) {}`
		- 对象创建之后指定
			`Object.defineProperty(obj, age, {get(){}, set(value){}})`
- watch 
	- 包含多个属性监视对象
	- Vue.$watch(propertyName,function(val){})
		- propertyName 要监视的属性名
		- 回调函数中形参是最新更新的数据
	- 分为一般监视和深度监视
		- 深度监视
			```
				'xxx' : {
					deep : true,
					handler : fun(value)
				}
			```

### vue 页面指令
- v-text/v-html -- 指定标签体
    - v-text -- 当作纯文本，相当于 {{}}
    - v-html -- 将 value 作为 html 标签来解析，相当于{{{}}}
    - 可以防止显示时闪屏
- v-el -- 为某个元素注册一个唯一标识, vue 对象可以通过 $els 属性访问这个元素对象
	- v-el:xxx
	- 读取得到标签对象 -- this.$els.xxx
	- HTML `<span v-el:msg>baidu</span>`
	- vm `this.$els.msg;`
- v-ref -- 标识组件
	- `ref=xxx`
	- 读取得到的标签对象 -- this.$refs.xxx
- v-model -- 在表单控件上创建双向绑定
	- 只限于 `input` / `select` / `textarea`
	- 表单项新特性指令
		- lazy -- 表单失去焦点时同步
		- number -- 将输入内容转换成 number 类型
		- debounce -- 设置一个最小的延时.在输入后延时同步
- v-if / v-else / v-show
    - v-if -- 如果 vlaue 为 true，当前标签会输出在页面中
	- v-else -- 与 v-if 一起使用，如果 value 为 false，将当前标签输出到页面中
	- v-show -- 根据表达式值的真假切换元素的 `display` CSS属性
	- template-- 模版标签，不会出现在页面上
	- 如果需要频繁切换 v-show 较好，如果在运行时条件不大可能改变 v-if 较好
- v-for -- 遍历
    - 遍历数组 -- `v-for="person in persons"` 
    - $index -- 当前数组元素的索引
    - 扩展数组方法-- 对数组的常用方法进行了包装(用于数据绑定)
		- $remove(item) -- 删除数组中对应的元素 (存在过滤索引会出错)
		- $set(index, ele) -- 给数组中指定下标指定对应的元素 
	- 遍历对象 -- `v-for="value in person"`  
	- $key -- 当前对象的属性名
- v-on -- 绑定事件监听
    - 格式 -- `v-on:事件名`
    - 简写 -- `@事件名`
    - 可指定参数也可不指定参数
    - 按键修饰符
	    - @keyup.keyCode   
	    - @keyup.enter
    - 事件修饰符
	    - @click.stop -- 阻止事件冒泡行为
	    - @click.prevent -- 阻止事件默认行为
    - 隐含对象 -- $event
- v-bind -- 强制数据绑定
	- `<img v-bind:src="imgSrc" alt="">`
    - 简写 -- 可直接省略v-bind只写冒号 `<img :src="imgSrc" alt="">`
    - 强制绑定不写冒号传的是字符串，写了冒号传的是变量 (动态的)
- v-cloak -- 使用它防止闪现表达式，与 css 配合
	- CSS --  `[v-cloak] {display: none}`
	- HTML --  `<p v-cloak>{{msg}}</p>`

### 自定义 vue 指令
#### 注册全局指令
- 代码
	```
		Vue.directive('my-directive', function(el, binding){
			el.textContent = binding.value.toupperCase();
		})
	```
- 参数
	- my-directive -- 自定义的指令名（去掉前缀'v-'）
	- 回调函数
		- el -- 指令所在的标签
		- binding -- 指令名等号右边的内容

#### 注册局部指令
- 在对象配置选项中注册
- 代码
	```
		directives : {
			'my-directive' : {
				bind (el, binding) {
					el.innerHTML = binding.value.toupperCase()
        		}
    		}
  		}
	```
- 参数
	- my-directive -- 自定义的指令名（去掉前缀'v-'，并加引号）
	- 回调函数
		- el -- 指令所在的标签
		- binding -- 指令名等号右边的内容

#### 使用指令
`v-my-directive='xxx'`

### vue 内置过滤器
- capitalize -- 首字母大写
- uppercase -- 全部大写
- lowercase -- 全部小写
- currency -- 货币化 (空格之后添加货币符号)
- pluralize -- 单数/复数处理
- json -- json格式化

### 自定义 vue 过滤器
#### 全局过滤器
- `Vue.filter`
- 代码
	```
		<!--过滤器reverse: 对指定值进行倒序显示-->
		<p>{{msg | reverse}}</p>

	    Vue.filter('reverse', function(value) {
	      //处理逻辑
	      return  value.split('').reverse().join('');
	    })
	```
- 参数
	- 第一个 -- 自定义过滤器名
	- 第二个 -- 过滤器回调，可传参数，回调函数必须 return 出结果

#### 局部过滤器
- 在对象配置选项中
- 代码
	```
		<!--过滤器wrap: 在指定值的左侧和右侧添加指定的文本-->
		<p>{{msg | wrap '左边的文本' '右边的文本'}}</p>

	    new Vue({
	      filters : {
	        'wrap' : function(value, left, right) {
	            //处理逻辑
	            return left + ' ' + value + ' ' + right;
	        }
	      }
	    })
	```
- 属性名 -- 过滤器名
- 属性值 -- 函数