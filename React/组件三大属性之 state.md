# 组件三大属性之 state
### state 简介
- 组件被称为“状态机”，通过更新组件状态值来更新对应的页面显示（重新渲染）

### this.state 初始化状态
```
	constructor (props) {
		super(props);
        this.state = {
			stateProp1 : value1,
          	stateProp2 : value2
    	};
	};
```

### 读取某个状态
`this.state.statePropertyName`

### this.setState({}) 更新状态
```
	this.setState({
		stateProp1 : value1,
		stateProp2 : value2
	})
```

### 实时切换更新页面案例
```
	class App extends React.Component{
		constructor(props){
			super(props);
        	this.state = {
				isHao:true //初始化状态
			};
			//修改this
			this.handleClick = this.handleClick.bind(this)
		}
    
		//定义点击方法
		handleClick()
			this.setState({
				isHao:!this.state.isHao //修改状态
			})
		};

		render(){
			let msg = this.state.isHao?'你好吗':'我不好';
			return (
				<p onClick={this.handleClick}>{msg}</p>
      		)
     	}
	}
  
    //渲染组件
    ReactDOM.render(<App/>,document.getElementById('example'))
```