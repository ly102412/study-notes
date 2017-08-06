# CSS 3 选择器
### 基本选择器
            
#### 子选择器
- 定义 -- 只能选择某元素的子元素
- 语法 -- 父元素 > 子元素
            
#### 相邻元素选择器               
- 定义 -- 可以选择紧接在此元素后的一个兄弟元素，而且他们具有相同的父元素
- 语法 -- 元素 + 相邻的兄弟元素
            
#### 通用兄弟元素选择器             
- 定义 -- 选择某元素后边的所有兄弟元素，而且他们具有同一个父元素
- 语法 -- 元素 ~ 后面所有兄弟元素
            
#### 群组选择器（分组选择器）
- 定义 -- 将具有相同样式的元素分在一起，每个选择器之间有逗号隔开
- 语法 -- 元素1，元素2，元素3……
        
#### 属性选择器           
- element[ attribute ]
	- 定义 -- 为带有 attribute 属性的元素设置样式
    - 语法 -- element[ attribute ]           
- element[ attribute = ’ value‘ ]
	- 定义 -- 为带有 attribute = ’ value‘ 属性的元素设置样式
    - 语法 -- element[ attribute = 'value' ]            
- element[ attribute~= ' value ' ]                
	- 定义 -- 选择 attribute 属性包含单词为 ’value‘ 的元素，并且设置样式
    - 语法 -- element[ attribute~= ' value ' ]            
- element[ attribute^= ' value ' ]               
	- 定义 -- 选择包含 attribute 属性，且其属性值以 value 开头的所有元素
    - 语法 -- element[ attribute^= ' value ' ]           
- element[ attribute$= ' value ' ]                
	- 定义 -- 选择包含 attribute 属性，且其属性值以 value 结尾的所有元素
    - 语法 -- element[ attribute$= ' value ' ]            
- element[ attribute*= ' value ' ]       
	- 定义 -- 选择包含 attribute 属性，且其属性值中包含 value 的所有元素
    - 语法 -- element[ attribute*= ' value ' ]
        
#### 伪类选择器            
- 动态伪类                
	- 定义 -- 这些伪类并不存在于 HTML 中，只有当用户和网站交互的时候才能体现出来              
	- 锚点伪类 -- ：link ， ：visited                
	- 用户行为伪类 -- ：hover ， ：active ，：focus
            
#### CSS 3 结构类（nth 选择器）（注：其中的 element 都是指子元素）
                
- first-child                    
	- 定义 -- 选择父元素的第一个子元素
    - 语法 -- element：first-child
- last-child
	- 定义 -- 选择父元素的最后一个子元素
    - 语法 -- element：last-child
    - （注：若其最后一个子元素不为 element 所代表的元素，则不做任何改变）               
- nth-child（n）                    
	- 定义 -- 选择某个元素下的第 n 个元素（注：n 是一个简单的表达式，不能用其他字母代替，可以使用类似 2n、3n 这种的表达式，n 虽然从 0 开始计算，但是 1 才代表第一个文字）                    
- nth-child（odd）-- 可用于匹配下标是奇数的元素的关键字                   
- nth-child（even）-- 可用于匹配下标是偶数的元素的关键字                    
	- 语法 -- element：nth-child                
- nth-last-child（n）                    
	- 定义 -- 选择某个元素中的第 n 个元素（注：从最后一个元素开始计算）
    - 语法 -- element：nth-last-child（n）              
- nth-of-type（n）
    - 定义 -- 选择父元素中指定类型的第 n 个子元素                    
	- 语法 -- element：nth-of-type（n）
- nth-last-of-type（n）
    - 定义 -- 选择父元素中指定类型的第 n 个子元素（注：从最后一个元素开始计算）                  
    - 语法 -- element：nth-last-of-type（n）
- first-of-type
    - 定义 -- 选择父元素中指定类型的首个子元素
    - 语法 -- element：first-of-type
- last-of-type
    - 定义 -- 选择父元素中指定类型的最后一个子元素
    - 语法 -- element：last-of-type
- only-child
    - 定义 -- 父元素只能有一个子元素且此子元素为指定的子元素
    - 语法 -- element：only-child
- only-of-type
   - 定义 -- 父元素可以有多个子元素，但其子元素中只有一个指定的类型
   - 语法 -- element：only-of-type
- empty
   - 定义 -- 匹配没有子元素（包括文本节点）的每个元素
   - 语法 -- element：empty    
- 否定选择器（：not）   
   - 定义 -- 匹配不是指定元素或选择器的每个元素 
   - 语法 -- 父元素  ：not（子元素或者选择器）
   - （注：父元素与否定选择器之间有空格）
- 伪元素（也可以使用 ：）
   - element：：frist-line
      - 定义 -- 对元素第一行文本进行设置，只能用于块级元素
   - element：：frist-letter
      - 定义 -- 用于向文本的首字母设置特殊的样式，只能用于块级元素
   - element：：before
      - 定义 -- 在元素内容前面插入新内容，与 content 配合使用
   - element：：after
      - 定义 -- 在元素内容后面插入新内容，与 content 配合使用
   - element：：selection
      - 定义 -- 用于设置浏览器中选中文本后的前景色与背景色
       
#### CSS 权重
- 定义 -- 当很多规则被应用到某一个元素上时，权重是一个决定哪种规则生效或者是优先级的过程
- 权重的等级与权值
   - 行内样式（1000） >  ID 选择器（100） > 类，属性选择器和伪类选择器（10） > 元素选择器和伪元素选择器（1） > 通配符选择器（0）
- CSS 权重规则
   - 当多个选择器发生冲突时，会选择权重高的选择器来显示，权重越高越优先显示
   - 比较时需要将多个选择器的权重相加在进行比较，如果权重一样，后面的会覆盖前面的样式
   - 权重相加不可能超过他的最大数量级，例如无论多少个元素选择器相加，都不可能超过一个 class 选择器的权重
   - 可以在样式后面添加一个！important ，这样该样式会拥有最大的优先级，其他样式都不能将其覆盖（注：尽量不要使用 ！important）