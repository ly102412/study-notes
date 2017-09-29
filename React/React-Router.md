# React-Router
### 路由简介
- 一个路由就是一个映射关系（key：value）
- key 为路由路径，value 可能是 function/component

### 路由分类
#### 后台路由
- node 服务器端的路由，value 是 function，用来处理客户端提交的请求并返回一个响应数据
- 注册路由 -- router.get(path,function(req,res,next))
	- path -- 路由的路径
	- req -- 获取请求参数
	- res -- 返回请求数据
	- next -- 调用后续的回调函数
- 当 node 接收到一个请求时，根据请求的路径找到匹配的路由，调用路由中的函数来处理请求，返回响应数据

#### 前端路由
- 浏览器的路由，value 是 component，当请求的是路由 path 时，浏览器端没有发送 http 请求，但界面会更新显示对应的组件
- 注册路由 -- <Route path="/about" component={About}>
- 当浏览器的 hash 值变为 #about 时，当前路由组件就会变成 About 组件
- 前端路由就是把不同路由对应的不同内容或页面的渲染任务交给前端去做（之前都是在服务器端进行渲染，并根据不同的 url 返回不同的页面）
- H5 的 history.pushState 和 history.repalceState 这两个 history 的新增的 API ，为前端操控浏览器历史栈提供了可能
	- 相同点 -- 这两个 API 都会操作浏览器的历史栈而不会引起页面刷新
	- 不同点 -- pushState 会增加一条新的历史记录，而 replaceState 则会替换当前的历史记录

### 应用 -- 单页面应用
#### 单页面应用简介
- 全称 single page web application，简称 SPA
- 整个应用只有一个完整的页面
- 单击页面中的链接不会刷新页面，本身也不会向服务器发请求
- 当点击链接时，只会做页面的局部更新
- 数据都需要通过 ajax 请求获取，并在前端异步展现

#### 优点与缺点
- 优点 -- 用户体验好，不需要每次向服务器发送请求请求页面数据，响应快
- 缺点 -- 使用浏览器的前进、后退键的时候会重新发送请求，没有合理利用缓存

### HASH 值
- 将任意长度的二进制字符串通过一定的算法映射成一个固定长度的较小的二进制字符串，这个字符串就是对应的 hash 值，主要特点就是唯一的，不可逆的
- hash 通常应用在 SPA 单页面应用中，通过不同的 hash 值映射的 url 可以使浏览器添加一条不同的 url 历史记录
- window.location.hash 
	- 读取时，可以用来判断网页状态是否改变
	- 写入时，则会在不重载网页的前提下创建一条访问历史记录
- window.onhashchange = fun -- 监听 hash 值的改变

### URl 中的 # 号
- `#` 代表网页中的一个位置，其右面的字符就是该位置的标识符
- `#` 是用来指导浏览器动作的，对服务器完全无用，所以，HTTP 请求中不包括 #
- 单单改变 # 后的部分，浏览器只会滚动到相应的位置，不会重新加载页面
- 这对于 ajax 应用程序特别有用，可以用不同的 # 值，表示不同的访问状态，然后向用户给出可以访问某个状态的链接
- window.location.hash -- 读取 # 值

### react-router 库中的相关组件
#### Router -- 路由器组件，用来包含各个路由组件
- 属性 -- history={hashHistory} 用来监听浏览器地址的变化
- hashHistory 是 react-router 提供的对象，保存了所有 hash 的 url
- 将 URL 解析成一个地址对象，供 React Router 匹配
- 子组件 -- Route

#### Route -- 路由组件，注册路由
- 属性1 -- path="/xxx"，映射请求的路由路径
- 属性2 -- component={Xxx}，请求的组件对象
- 根路由组件 -- path="/"，通常对应的是主组件
- 子路由组件 -- 子 <Route> 配置组件

#### IndexRoute -- 默认路由组件
- 当父路由组件被请求时，默认就会请求此路由组件

#### hashHistory -- 路由的切换由URL的hash变化决定，即URL的#部分发生变化
- 用于 Router 组件的 history 属性
- 作用 -- 为地址 url 生成 ?_k=hash，用于内部保存对应的 state

#### Link -- 路由链接组件
- a 标签用 Link 标签代替，从 react 里取得 {Link}
- 属性1 -- to="/xxx"，要请求的路由路径
- 属性2 -- activeClassName="active"，活动时触发的 class 名

### 基于脚手架创建项目
#### 下载
`npm install react-router --save`
#### 定义各个路由组件
- About.js
	```
		import React from 'react'
		function About() {
			return <div>About组件内容</div>
		}
		export default About
	```
- Home.js
	```
		import React from 'react'
		function Home() {
			return <div>Home组件内容2</div>
		}
		export default Home
	```
- Repos.js
	```
		import React, {Component} from 'react'
		export default class Repos extends Component {
			render() {
				return (
					<div>Repos组件</div>
				)
			}
		}
	```
- App.js
	```
		import React, {Component} from 'react'
		import {Link} from 'react-router'
    
		export default class App extends Component {
			render() {
				return (
					<div>
						<h2>Hello, React Router!</h2>
						<ul>
							<li><Link to="/about" activeClassName="active">About2</Link></li>
							<li><Link to="/repos" activeClassName="active">Repos2</Link></li>
						</ul>
						{this.props.children}
					</div>
				)
      		}
		}
	```

#### index.js -- 注册路由，渲染路由器标签
```
	import React from 'react'
    import {render} from 'react-dom'
    import {Router, Route, IndexRoute, hashHistory} from 'react-router'
    import App from './modules/App'
    import About from './modules/About'
    import Repos from './modules/Repos'
    import Home from './modules/Home'
    
    render((
      <Router history={hashHistory}>
        <Route path="/" component={App}>
          <IndexRoute component={Home}/>
          <Route path="/about" component={About}></Route>
          <Route path="/repos" component={Repos}></Route>
        </Route>
      </Router>
    ), document.getElementById('app'))
```

#### 主页面 -- index.js
```
	<style>
      .active {
        color: red;
      }
    </style>
```

#### 向路由组件传递请求参数
- repo.js -- repos组件下的分路由组件
	```
    	import React from 'react'
    	export default function ({params}) {
      		let {username, repoName} = params
      		return (
        		<div>用户名:{username}, 仓库名:{repoName}</div>
      		)
    	}
	```

- repos.js
	```
    	import React from 'react'
    	import NavLink from './NavLink'
    
	    export default class Repos extends React.Component {
	    
	      constructor(props) {
	        super(props);
	        this.state = {
	          repos: [
	            {username: 'faceback', repoName: 'react'},
	            {username: 'faceback', repoName: 'react-router'},
	            {username: 'Angular', repoName: 'angular'},
	            {username: 'Angular', repoName: 'angular-cli'}
	          ]
	        };
	        this.handleSubmit = this.handleSubmit.bind(this)
	      }
	    
	      handleSubmit () {
	    
	        const repos = this.state.repos
	        repos.push({
	          username: this.refs.username.value,
	          repoName: this.refs.repoName.value
	        })
	        this.setState({repos})
	        this.refs.username.value = ''
	        this.refs.repoName.value = ''
	      }
	    
	      render() {
	        return (
	          <div>
	            <h2>Repos</h2>
	            <ul>
	              {
	                this.state.repos.map((repo, index) => {
	                  const to = `/repos/${repo.username}/${repo.repoName}`
	                  return (
	                    <li key={index}>
	                      <Link to={to} activeClassName='active'>{repo.repoName}</Link>
	                    </li>
	                  )
	                })
	              }
	              <li>
	                <form onSubmit={this.handleSubmit}>
	                  <input type="text" placeholder="用户名" ref='username'/> / {' '}
	                  <input type="text" placeholder="仓库名" ref='repoName'/>{' '}
	                  <button type="submit">添加</button>
	                </form>
	              </li>
	            </ul>
	            {this.props.children}
	          </div>
	        );
	      }
	    }
	```
- index.j -- 配置路由
	```
	    <Route path="/repos" component={Repos}>
	      <Route path="/repos/:username/:repoName" component={Repo}/>
	    </Route>
	```

#### 优化Link组件
- NavLink.js
	```
	    import React from 'react'
	    import {Link} from 'react-router'
	    export default function NavLink(props) {
	      return <Link {...props} activeClassName="active"/>
	    }
	```
- Repos.js
    `<NavLink to={to}>{repo.repoName}</NavLink>`
    
 
 