# jQuery 插件
### jQuery 日期插件 -- layDate
#### 插件的基本使用
```
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>01_laydate插件的基本使用</title>
	    <script src="laydate/laydate.js"></script>
	</head>
	<body>
	    <input placeholder="请输入日期" class="laydate-icon" onclick="laydate()">
	    <br>
	    <input placeholder="请输入日期" id="hello1">
	    <span class="laydate-icon" onclick="laydate({elem: '#hello1'});"></span>
	</body>
	</html>
```
#### layDate API 选项
- elem: '#id',    //需显示日期的元素选择器
- event: 'click', //触发事件
- format: 'YYYY-MM-DD hh ss',  //日期格式
- istime: false,  //是否开启时间选择
- isclear: true,  //是否显示清空
- istoday: true,  //是否显示今天
- issure: true,   //是否显示确认
- festival: true, //是否显示节日
- min: `1900-01-01 00:00:00`, //最小日期
- max: `2099-12-31 23:59:59`, //最大日期
- start: `2014-6-15 23:00:00`, //开始日期
- fixed: false, //是否固定在可视区域
- zIndex: 99999999,  //css z-index
- choose: function(dates){}  //选择好日期的回调

#### 插件的高级使用
```
	<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <title>02_laydate插件的高级使用</title>
		    <script src="jquery-1.11.3.js"></script>
		    <script src="laydate/laydate.js"></script>
		</head>
		<body>
		    <input id="mydate" placeholder="请输入日期" class="laydate-icon">
		    <script>
		        laydate({
		            elem : "#mydate",
		            event : "focus",
		            istime : true,
		            isclear : false,
		            istoday : false,
		            issure : false
		        });
		    </script>
		</body>
		</html>
```

### 表单验证插件
#### 常用的验证插件
- formValidator
- jQuery.validator
- easyForm
- validate.js

#### jQuery.validator 插件
- 引入必要的文件
	- 引入 jQuery 库文件
	- 引入插件文件 dist/jquery.validate.js
	- 引入国际化文件（提示语言文件）
		- dist--localization--message_zh.js 中文提示语言
- 在HTML页面定义表单
	- 表单的元素使用 HTML5 提供的新表单验证功能
	- required 表示必填项
- 在JS逻辑中填写
	- 通过表单调用 validate() 核心方法 -- $().validate()

#### validation 的基本使用
```
	<div id="main">
		<p>Take a look at the source to see how messages can be customized with metadata.</p>
	    <!-- Custom rules and messages via data- attributes -->
	    <form class="cmxform" id="commentForm" method="post" action="">
	        <fieldset>
	            <legend>Please enter your email address</legend>
	            <p>
	                <label for="cemail">E-Mail *</label>
	                <input id="cemail" name="email" data-rule-required="true" data-rule-email="true" data-msg-required="Please enter your email address" data-msg-email="Please enter a valid email address">
	            </p>
	            <p>
	                <input class="submit" type="submit" value="Submit">
	            </p>
	        </fieldset>
	    </form>
	</div>
	<script>
	    $(document).ready(function() {
	        $("#commentForm").validate();
	    });
	</script>
```

##### validation 自定义验证
- $().validate(options)
- rules -- 自定义的验证规则
	- key -- 要验证的表单元素的name属性值
	- value -- 指定使用的验证规则名称
	- 实例代码
		```
			rules : {
			   email:true, //输入正确的email格式
			   number:true, //输入合法的数字
			}
		``` 
- equalTo -- 相同内容的id
- messages -- 自定义的错误提示
	- 实例代码
		```
			messages : {
				key : ' value '
			}
		```
- 自定义错误提示的显示位置(单选和多选框)
	- 自定义的错误提示默认出现在第一个被验证的元素后面
	- 自定义的错误提示应该出现在一组验证元素的后面
	- 自定义了用于显示错误提示信息的标签
		- `<label for="" class="error"></label>`
		- class 插件底层的错误提示信息的样式
		- for 告知插件当前错误提示信息与哪个指定的验证元素相关
		
#### 自定义验证的方法
- jQuery.validator.addMethod( name, method [, message ] )方法
	- name：设置验证方法的名称。
	- method：回调函数，function(value,element,param){}
	    - value：元素的值
	    - element：元素本身
	    - param：参数
	- message：设置验证不通过的错误提示信息。



		