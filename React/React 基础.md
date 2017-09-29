# ReactJS
### React 简介
- Facebook 开源的一个 JS 库
- 一个用于动态构建用户界面的 JS 库

### React 的特点
- Declarative（声明式编码）
- Component-Based（基于组件化的开发）
- Learn Once，Write Anywhere（支持客户端与服务器端渲染）
- 高效
- 单向数据流

### React 高效的原因
- 虚拟（virtual）DOM，不总是直接操作 DOM
- 高效的 DOM Diff 算法，最小化页面重绘

### 模块与组件
#### 模块
- 理解 -- 向外提供特定功能的 JS 程序，一般就是一个 JS 文件
- 为什么使用模块 -- JS 代码更多更复杂
- 作用 -- 复用 JS，简化 JS 的编写，提高 JS 的运行效率

#### 组件
- 理解 -- 用来实现特定功能效果的代码集合（html/css/js）
- 为什么使用组件 -- 一个界面的功能太复杂
- 作用 -- 复用编码，简化项目界面编码，提高运行效率 

![组件](http://i.imgur.com/YnVjluG.jpg)

### 模块化与组件化
#### 模块化
- 当应用的 JS 都以模块来编写时，这个应用就是一个模块化应用

#### 组件化
- 当应用是以多组件的方式实现功能时，这个应用就是一个组件化的应用

### 相关的 JS 库
- react.js -- React 的核心库（优先引入）
- react-dom.js -- 提供操作 DOM 的扩展库
- babel.min.js -- 将 JSX 语法代码转为纯 JS 语法代码的库

### React 的基本编码
- HTML 页面创建 DOM 容器
	`<div id="container"></div>`
- script 标签
	`<script type="text/babel"></script>`
- 创建虚拟 DOM 元素
	`let element = <h2>hello react</h2>`
- 渲染虚拟 DOM 对象
	`ReactDOM.render(element,document.getElementById('container'))`

### JSX -- JavaScript XML 
- react 定义的一种类似于 XML 的 JS 扩展语法： XML + JS
- 作用 -- 用来创建 React 虚拟 DOM （元素）对象
	- 例：`var ele = <h1>Hello JSX</h1>`
	- 注意一：他不是字符串，也不是 HTML/XML 标签
	- 注意二：他最终产生的就是一个 JS 对象
- 标签名任意 -- HTML 标签或其他标签
- 标签属性任意 -- HTML 标签属性或其他属性
- 基本语法规则一
	- 遇到以 "<" 开头的代码以标签的语法解析
	- HTML 同名标签转换为 HTML 同名元素
	- 其他的标签需要特别的解析（必须是一个闭合标签）
	- 标签的 class 属性必须改为 className 属性
	- 标签的 style 属性必须写为：{{color：'red',display:'none'}}
- 基本语法规则二
	- 遇到以 "{" 开头的代码，以 JS 的语法解析
	- 标签中的 JS 代码必须用大括号包裹
- babel.js 的作用
	- 浏览器的 JS 引擎是不能直接解析 JSX 语法代码的，需要 babel 转译为纯 JS 的代码才能运行
	- 只要用了 JSX，都要将 script 标签中的 type 改写为 type="text/babel"，声明需要 babel 来处理

### 虚拟 DOM
- 一个虚拟 DOM （元素）是一个一般的 JS 对象，准确的说是一个对象树（倒立的）
- 虚拟 DOM 保存了真实 DOM 的层次关系和一些基本属性，与真实的 DOM 一一对应
- 如果只更新了虚拟 DOM，页面不会重绘
- 虚拟 DOM 对象最终都会被 React 转换为真实的 DOM
- 编码时基本只需要操作 React 的虚拟 DOM 的相关数据，React 会转换为真实 DOM，会因真实 DOM 的变化而更新界面
- 虚拟 DOM 本质上就是在 JS 和 DOM 之间做了个缓存

### 创建虚拟 DOM
- React.createElement('h1', {id:'myTitle'}, title)
	- 第一个参数 -- 标签的类型
	- 第二个参数 -- 配置对象（标签的属性）
	- 第三个参数 -- 内容
	- 纯 JS（一般不用）
- JSX 
	`<h1 id='myTitle'>{title}</h1>`

### 渲染虚拟 DOM
- 语法 -- ReactDOM.render(virtualDOM,containerDOM)
- 作用 -- 将虚拟 DOM 元素渲染到真实容器 DOM 中显示
- 参数
	- 参数一：纯 JS 或 JSX 创建的虚拟 DOM 对象
	- 参数二：用来包含虚拟 DOM 元素的真实 DOM 元素对象（一般是一个 div）

### 自定义组件标签（Component）
- 内部组件不可以直接继承外部组件 props 中的内容
- 外部组件可以向内部组件传递数据（通过 props）
- 外部组件可以看到内部组件
- 内部组件看不到外部组件不可以直接传递数据

### 自定义组件的方式
#### 工厂（无状态）函数（简单组件，推荐使用）
```
	function MyComponent1() {
		return <h1>自定义组件标题11111</h1>
	}
```
> 注意事项
> 返回虚拟 DOM 对象
> 通常用来定义简单组件
> 无状态

#### ES6 类语法（复杂组件，推荐使用）
```
	class MyComponent3 extends React.Component {
      render () {
        return <h1>自定义组件标题33333</h1>
      }
    }
```
> 注意事项
> 返回虚拟 DOM 对象
> 通常定义复杂的组件
> 继承于 react 核心组件`React.Componet`
> 使用 `render(){}` 需要 return 返回
> 多个标签写到 `return()` 括号里并用 div 根标签包裹

#### ES5 老语法（不推荐使用）
```
	var MyComponent2 = React.createClass({
      render () {
        return <h1>自定义组件标题22222</h1>
      }
    })
```

#### 注意事项
- 返回的组件类必须首字母大写
- 虚拟DOM元素必须只有一个根元素
- 虚拟DOM元素必须有结束标签

#### 渲染组件标签
` ReactDOM.render(<MyComponent/>, document.getElementById('example'))`

#### ReactDOM.render() 渲染组件标签的基本流程
- React 内部会创建组件实例对象
- 得到包含的虚拟 DOM 并解析为真实 DOM
- 插入到指定的页面元素内部

