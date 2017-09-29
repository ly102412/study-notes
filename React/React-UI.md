# React-UI
### 常用的 UI 库
- material-ui -- 国外常用
- ANT DESIGN -- 国内常用

### ant-design 使用
#### 使用 create-react-app 搭建 react 开发环境
```
	npm install create-react-app -g
	create-react-app antd-demo
	cd antd-demo
	npm start
```

#### 搭建 antd 的基本开发环境
- 下载
	`npm install antd --save`
- src/App.js
	```
		import React, { Component } from 'react';
	    import { Button } from 'antd';
	    import './App.css';
	    
	    class App extends Component {
	      render() {
	        return (
	          <div className="app">
	            <Button type="primary">Button</Button>
	          </div>
	        );
	      }
	    }
    	export default App;
	```

- src/App.css
	```
		@import '~antd/dist/antd.css';
	    
	    .app {
	      text-align: center;
	    }
	```

#### 实现按需加载（组件 js/组件 css）
- 使用 eject 命令将所有内建的配置暴露出来
	`npm run eject`
- 下载 babel-plugin-import(用于按需加载组件代码和样式的 babel 插件)
	`npm install babel-plugin-import --save-dev`
- 修改配置 -- config/webpack.config.dev.js
	```
		// Process JS with Babel.
	    {
	      test: /\.(js|jsx)$/,
	      include: paths.appSrc,
	      loader: 'babel',
	      options: {
          +   plugins: [
          +     ['import', { libraryName: 'antd', style: 'css' }],
          +   ],
              // This is a feature of `babel-loader` for webpack (not Babel itself).
              // It enables caching results in ./node_modules/.cache/babel-loader/
              // directory for faster rebuilds.
              cacheDirectory: true
            }
		 },
	```
- 去除引入全量样式的语句 -- src/App.css
	`@import '~antd/dist/antd.css'` 
