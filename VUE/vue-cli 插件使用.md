# vue-cli 插件使用
### 说明
- vue-cli是vue官方提供的脚手架工具
- github: https://github.com/vuejs/vue-cli

### 使用 vue-cli 快速创建工程化 vue 项目
#### 使用基于 webpack 的简单模板创建项目
```
	npm install -g vue-cli    //全局下载脚手架包
    vue init webpack-simple webpack-simple_demo   //下载模板
    cd webpack-simple_demo
    npm install
    npm run dev
    访问: http://localhost:8080/
```

#### 使用基于 webpack 的完整模板创建项目
```
	vue init webpack webpack_demo
    cd webpack_demo
    npm install
    npm run dev
    访问: http://localhost:8080/
```

#### 模板项目的结构
```
	|-- build : webpack相关的配置文件夹(基本不需要修改)
    	|-- dev-server.js : 通过express启动后台服务器
	|-- config: webpack相关的配置文件夹(基本不需要修改)
    	|-- index.js: 指定的后台服务的端口号和静态资源文件夹
	|-- node_modules
	|-- src : 源码文件夹
    	|-- components: vue组件及其相关资源文件夹
      	|-- app.vue: 应用根主组件
    	|-- main.js: 应用入口js
	|-- static: 静态资源文件夹
	|-- .babelrc: babel的配置文件
	|-- .eslintignore: eslint检查忽略的配置
	|-- .eslintrc.js: eslint检查的配置
	|-- .gitignore: git版本管制忽略的配置
	|-- index.html: 主页面文件
	|-- package.json: 应用包配置文件 
	|-- README.md: 应用描述说明的readme文件
```

### 编码测试与打包发布项目
#### 编码测试
```
	npm run dev
    访问: http://localhost:8080
    编码, 自动编译打包(HMR), 查看效果
```
> 注
> HMR 热模替换 -- 不刷新全部页面，只刷新更改的地方，可以立即查看效果

#### 打包发布
```
	npm run build
    npm install -g pushstate-server
    pushstate-server dist
    访问: http://localhost:9000
```