# 组件三大属性之 refs
### refs 简介
- 组件内的标签都可以定义 ref 属性来标识自己
- 在组件中可以通过`this.refs.ref属性名`的方式得到对应的真实 DOM 对象
- 作用 -- 用于操作指定的 ref 属性的 DOM 元素对象（表单标签居多）
- 例
	`<input ref='username'>`
	`this.refs.username`

### 事件处理
- 通过 onXxx 属性指定组件的事件处理函数（注意大小写）
- React 使用的是自定义（合成）事件，而不是使用的 DOM 事件
- React 中的事件是通过事件委托方式处理的（委托给组价最外层的元素）
- 必须通过 this 把事件绑定给组件的实例对象（不需要调用）
- 通过 event.target 得到发生事件的 DOM 元素对象

### this 的注意事项
- 组件内置的方法中的 this 为组件对象
- 在组件中自定义的方法中的 this 为 null
- 解决方法
	- 使用类的继承控制器对象强制绑定 this
		- 代码实现
			```
				constructor(props){
				   super(props)
				   this.xxx = this.xxx.bind(this)
			    }
			```
	- 箭头函数 --  ES6 模块化编码时才能使用

### 自定义组件实现弹框显示输入信息
```
    //创建组件
    class App extends React.Component{
      constructor(props){
        super(props);

        //修改this(this指向肯定是组件类的实例对象)
        this.handleClick = this.handleClick.bind(this)
      }


      //定义点击事件的方法
      handleClick(){
        let value = this.refs.msg.value;
        alert(value)
      }
      //定义失去焦点的方法
      handleBlur(event){
        let value = event.target.value;
        alert(value)
      }
      render(){
        return (
            <div>
              <input type="text" ref="msg"/>
              <button onClick={this.handleClick}>提示输入数据</button>
              <input onBlur={this.handleBlur} type="text" placeholder="失去焦点显示数据"/>
            </div>
        )
      }
    }
    
    //渲染
    ReactDOM.render(
        <App/>,
        document.getElementById('example')
    )
```
