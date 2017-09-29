# 组件三大属性之一 -- props
### props 简介
- 每个组件实例对象都会有 props 属性（properties 的缩写）
- 组件标签的所有属性都保存在 props 中
- 作用 -- 通过标签属性从组件外部向内部传递只读数据（不可修改 props 属性）
- 在组件内部读取属性
	- this.props.属性名
	- 实例代码
		```
			class Person extends React.Component{
	        	render(){
	          		return (
	              		<ul>
	                		<li>姓名: {this.props.name}</li>
	                		<li>年龄: {this.props.age}</li>
	                		<li>性别: {this.props.sex}</li>
	              		</ul>
	          		)
	        	}
	      	}
		```

### 定义组件的默认 props 属性
- 组件实例.defaultProps = {}
- 实例代码
	```
		Person.defaultProps = {
			age: 18,
            sex: '男'
		};   
	```

### 规定组件 props 属性的数据类型和必要性 
- 组件实例.propTypes = {}
- isRequired -- 表示必填项
- 实例代码
	```
		Person.propTypes = {
	        name: React.PropTypes.string.isRequired,
	        age: React.PropTypes.number
		}
	```

### 扩展属性 -- 定义对象的所有属性通过 props 传递
- 利用三点运算符把定义的对象全部属性传入虚拟 DOM 标签里
- <组件实例对象 {...定义对象}/>
- 实例代码
	```
		let person1 = {name:'dirk',age:41,sex:'男'};
	          
		ReactDOM.render(
			<Person  {...person1}/>,
	        document.getElementById('example2')
	    )
	```

### 组件类的构造函数
```
	constructor (props) {
      super(props);
      console.log(props); // 查看所有属性
    }
```

### 拆分组件
- 拆分组件 -- 拆分页面，抽取组件
	- 主组件 -- APP
	- 子组件 -- Welcome
- 确定组件中的 props
	- APP -- names/array
	- Welcome -- name/string
- 实例代码
	```
		//定义Welcom组件
		function Welcome(props) {
			return <h2>Welcome {props.name}</h2>
		}
    
		//定义app组件 外层
		class App extends React.Component{
			render(){
				return (
					<div>
						{
							this.props.names.map((item,index)=>{return <Welcome key={index} name={item}/>})
						}
            		</div>
          		)
        	}
		}
    
		let names = ['tom','jason','bob'];
		//渲染组件
		ReactDOM.render(
			<App names= {names}/>,
			document.getElementById('example')
		)
	```

