# eslint 
### 说明
- ESLint是一个代码规范检查工具
- 官网: http://eslint.org/
- 基本已替代以前的JSLint

### ESLint 提供以下支持
- ES6
- AngularJS
- JSX
- style 检查
- 自定义错误和提示

### ESLint 提供以下几种校验
- 语法错误校验
- 不重要或丢失的标点符号，如分号
- 没法运行到的代码块
- 未被使用的参数提醒
- 确保样式的统一规则，如 sass 或 less
- 检查变量的命名

### 规则的错误等级有三种
0 -- 关闭规则
1 -- 打开规则，并且作为一个警告（不影响代码运行）
2 -- 打开规则，并且作为一个错误（代码不能运行）

### 相关配置文件
#### .eslintrc.js 
- 规则的全局配置文件，可以在此修改规则
- 实例
	```	
		'rules': {
      		'no-new': 1   
    	}
	```

#### 在 js/vue 文件中修改局部规则
- 实例
	```
		/* eslint-disable no-new */
		new Vue({
			el: 'body',
			components: { App }
		})
	```

#### .eslintignore: 指令检查忽略的文件,　可以在此添加想忽略的文件
- `*.js`
- `*.vue`