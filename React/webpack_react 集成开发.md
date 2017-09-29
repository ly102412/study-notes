# webpack_react 集成开发
### 项目初始化
```
	|- src------------源码文件夹   
		|- js---------------js源文件夹
		|- css--------------css源文件夹
		App.js ----------- React主组件
	|- index.html-----页面文件
	|- webpack.config.js ---- 配置文件
	|- package.json---项目包配置文件
		{
			"name": "webpack_react",
			"version": "1.0.0"
		} 
```

### 下载相关模块包
- react 相关库
	`npm install react react-dom --save`
- babel 相关库
	`npm install babel-core babel-preset-es2015 babel-preset-react --save-dev`
- webpack 相关库
	`npm install webpack@1.13.0 babel-loader --save-dev`
	`npm install webpack-dev-server@1`
- css 加载器
	`npm install style-loader css-loader --save-dev`

### webpack 配置文件 -- webpack.config.js
```
	module.exports = {
		//入口js
		entry: "./src/js/main.js",
		//输出
		output: {
			path: __dirname,
			filename: "./dist/bundle.js"
		},
		  
		module: {
			loaders: [
				//babel处理js
				{
		          test: /\.js?$/,
		          exclude: /node_modules/, //排除此文件夹
		          loader: 'babel-loader'
		        },
		        //处理css
		        {
		          test: /\.css$/,
		          loader: 'style-loader!css-loader'
		        }
			]
		}
	}
```

### babel 配置文件 -- .babelrc
```
	{
		"presets": ["es2015", "react"]
	}
```

### 编码
- 	src/App.js -- 应用组件
```
		import React from 'react'
		export default function App() {  //暴露组件都得使用默认暴露
			return <h1>Hello React Client Component</h1>
		}
```

- src/js/main.js -- 入口js
```
	import React from 'react'
	import ReactDOM from 'react-dom'
	import App from '../App'
	//渲染组件标签到页面元素
	ReactDOM.render(<App />, document.getElementById('demo'))
```
- index.html
```
	<div id="container"></div> <!-- 设置react主组件容器-->
	<script type='text/javascript' src='dist/bundle.js'></script>
```
-  src/css/test.css
```
	body{
		background : red
	}
```
- webpack.confg.js -- 配置热加载
```
	devServer:{
		contentBase: './',//内置服务器动态加载页面所在的目录
		historyApiFallback:true,//不跳转
		inline:true
	}
```

### 运行命令
- 构建任务 -- webpack
- 热加载任务 -- webpack-dev-server

### package.json -- 添加编译/运行脚本
```
	"scripts": {
		"start": "webpack-dev-server --contentbase src --inline --hot",
		"build": "webpack"
	}
```