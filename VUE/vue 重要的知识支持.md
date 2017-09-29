# vue 重要的知识支持
### [ ].slice.call（伪数组对象）
- 将伪数组转换为真数组
- 实例
	```
		lis = [].slice.call(lis); 
		console.log(lis instanceof Array);  //true
	```

### nodeType 
- 获取节点类型
- Element 元素节点 -- 1
- Attr 属性节点 -- 2
- text 文本节点 -- 3

### Object.defineProperty(obj,propertyName,{})
- 给对象添加/修改属性（指定描述符）
- 参数 -- 要添加的对象 / 添加的属性名 / 配置属性对象
- 数据描述符
	- configurable: true/false -- 是否可以重新define
	- enumerable: true/false -- 是否可以枚举
	- value -- 指定初始值
	- writable: true/false -- value是否可以修改
- 存取（访问）描述符
	- get -- 回调函数，用来得到当前属性值，当读取属性值时就会自动调用
	- set -- 函数，用来监视当前属性值的变化，当属性值发生了变化时自动调用

### obj.hasOwnProperty(prop)
- 判断某属性是否是 obj 自身的属性
- prop 是字符串类型
### Object.keys(obj)
- 得到对象自身可枚举属性组成的数组
### DocumentFragment 
- 文档碎片
- 高效批量更新多个节点
- 通过`document.createDocumentFragment()`，创建 fragment 对象
- 实例
	```
	[初始文本]
	<ul id="fragment_test">
	  <li>test1</li>
	  <li>test2</li>
	  <li>test3</li>
	</ul>

	// 创建空的 fragment 对象
	var fragment = document.createDocumentFragment();
	// 获得ul
 	var ul = document.getElementById('fragment_test');

	//剪切ul下的所有子节点到 fragment 对象里
	var child = null;
	while(child = ul.firstChild) {
	  fragment.appendChild(child)
	}
	console.log(fragment); 
  
    //遍历 fragment 中所有的child. 将元素类型的child更新 标签体文本
    var children = fragment.childNodes;
    console.log(children.length); // 7个
    [].slice.call(children).forEach(function (child, index) {
      if (child.nodeType === 1) { //找到所有元素节点
        child.innerHTML = 'fragment'
      }
    });

    // fragment对象里的元素 粘贴进ul里
    ul.appendChild(fragment);

	[页面新的文本]
	fragment
	fragment
	fragment
	```

### 编写项目的方式
- 模块化 -- 以 js 文件编写
- 组件化
	- 一个组件标签就代表一个组件对象
	- 编写复杂界面拆分成各个组件并组合使用
- 工程化
	- 通过命令自动化构建项目
	- 如果项目构建是自动化的，就是工程化
	
#### 模块和组件
- 模块 -- JS 文件（实现特定的功能）
- 组件 -- 功能模块（界面由很多组件组成）
	- 组件里可能包含多个 JS 模块
	- 包含实现页面功能的所有资源