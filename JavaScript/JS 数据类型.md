# JS 数据类型
### 数据类型的分类
- 原始类型
	- string -- 字符串
	- number -- 数字
	- boolean -- 布尔类型
- 包装类型
	- String
	- Number
	- Boolean
- 引用类型
	- Object
- 特殊类型
	- undefined
	- null
- 注：string，number，boolean，null，undefined 属于基本数据类型； object 属于引用数据类型

### typeof 关键字
- 通过 typeof 可以检测一个变量的数据类型
- 返回值是一个字符串，用来描述数据类型
- 使用typeof检查一个字符串时，会返回string
- 使用typeof检查一个数值时，会返回number
- 使用typeof检查一个布尔值时，会返回boolean
- 使用typef检查一个 Null（空值）时，会返回Object
- 使用typeof检查一个未定义值时，会返回Undefined

### 原始数据类型
#### string 字符串
- 在JS中字符串需要使用引号引起来（单引号双引号都可以）
- 引号不可以被嵌套
- 当需要打印一些特殊字符时，可以使用 \ 来作为转义字符
	- 例
		- \" -- 表示“ ”
	    -  \‘ -- 表示‘ ’
	    - \\ -- 表示 \
	    - \t -- 表示制表符 （tab键）
	    - \n -- 表示换行
	    - \uxxxx -- 表示一个unicode编码. xxxx代表编码数值

#### number 数值
- 在 JS 中所有的数字都是 number 类型
- 包括整数和浮点数
- 在 JS 中尽量不要做对精确度要求很高的计算，计算浮点数会出现不可预期的结果
- Number.MAX_VALUE来获取最大值
	- 1.7976931348623157e+308
- Number.MIN_VALUE 0以上的最小值：
	- 5e-324
- infinity -- 无穷大
	- 数据类型也是 number
- NaN -- not a number
	- 表示非法数字
	- 数据类型也是 number

#### boolean 布尔值
- 使用布尔值进行逻辑判断
- 布尔值只有两个 true 和 false
- true 表示逻辑为真
- false 表示逻辑为假

### 包装类型
#### String 类型
- 原始类型 string -- 字面量/直接量（使用 typeof 运算符对原始类型返回“string”）
- 包装类型 String -- 创建对象（使用 typeof 运算符对包装类型返回“object”）

#### Number 类型
- 原始类型 number -- 字面量/直接量（使用 typeof 运算符对原始类型返回“string”）
- 包装类型 Number -- 创建对象（使用 typeof 运算符对包装类型返回“object”）
   
#### Boolean 类型
- 原始类型 boolean -- 字面量/直接量（使用 typeof 运算符对原始类型返回“string”）
- 包装类型 Boolean -- 创建对象（使用 typeof 运算符对包装类型返回“object”）

#### 包装类型的语法结构
- var 变量名 = new String（文本内容）

#### instanceof 关键字
- 类似于 typeof 关键字的作用，用于判断当前值的类型
- 语法结构
	- 当前值（变量） instanceof 包装类型的名称
	- 结果
		- true -- 说明当前值是指定的包装类型
		- false -- 说明当前值不是指定的包装类型

#### 原始类型与包装类型的关系
- 原始类型是包装类型的实例对象（包装类型表示一个大类，原始类型表示包装类型大类中的某一个）

### 特殊类型
#### undefined
- 含义 -- 表示未定义
- undefined 类型只有一个值，那就是 undefined
- 得到 undefined 的情况
	- 只声明但不赋值
	- 既声明也赋值，但赋的值是 undefined
    - 函数中不明确指定 return 
    - 访问一个对象不存在的属性
    
#### null
- 含义 -- 表示空
- null 是 object 类型中的一个特殊值
- 作用 -- 释放资源
- 注：null 只是一个值，而不是类型

### JS 数据类型转换
#### 转换为 String
- 调用 toString() 方法
	- null 和 undefined 不能使用
- 调用 String() 函数
	- null 转换成 “null”
	- undefined 转换为 “undefined”
- 任意值 = 任意值 + ""

#### 转换为 Number
- 使用 Number() 函数
	- 如果字符串是合法的数字则转换成对应数字
	- 如果字符串不是合法数字则转换成 NaN
	- 如果字符串是空串或者是空格则转换为 0
	- true 转换为 1 
	- false 转换为 0
	- null 转换为 0 
	- undefined 转换为 NaN
- 使用 parseInt() 或 parseFloat()
	- parseInt() 将字符串转换成整数
	- parseFloat() 将字符串转换为小数
	- 如果在这两个函数中传递一个非字符串作为参数会变成 NaN
- 任意值 = + 任意值
	- 进行任何计算也可转换

#### 强制类型转换为Boolean
- 使用 Boolean() 函数
	- 对于字符串除了空串是 false,其余都是 true
	- 对于数字除了 0 和 NaN 是 false,其余都是 true
	- 对于 Null,转换成 false
	- 对于 undefined,转换成 false
	- 任何对象默认都是 true
- 任意值 = !!任意值


