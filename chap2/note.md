- 基本选择器与层次选择器

选择器名称 | 语法 | 选择器名称 | 语法 | 选择器名称 | 语法
---|---|---|---|---|---
标签 | E{} | ID | #E{} | 类 | .E{}
群组 | E,F,G{} | 后代 | E F{} | 通配 | *{}
伪类 | E: PseudoElements{} | 子 | E>F{} | 临近 | E+F{}
属性 | E[attr]{} | 后兄弟节点 | E ~ F{} |  | 

- 基本过滤选择器

选择器名称 | 语法 | 选择器名称 | 语法 
---|---|---|---|---|---
第一个元素| :first | 最后一个元素 | :last 
偶数索引 | :even | 奇数索引 | :odd
索引大于index | :gt(index) | 索引小于index | :lt(index) 
获取焦点的元素 | :focus | 索引等于index | :eq(index) 
所有的标题元素 | :header | 所有正在执行的动画 | :animated 
去除所有与给定选择器匹配的元素 | :not(selector) | |

- 内容选择器

选择器名称 | 语法 | 选择器名称 | 语法 
---|---|---|---|---|---
含有文本内容text | :contains(text) | 不含子元素或文本 | :empty 
含有与选择器匹配的元素的元素 | :has(selector) | 含有子元素或文本 | :parent

- 可见性过滤选择器

选择器名称 | 语法 | 选择器名称 | 语法 
---|---|---|---|---|---
所有不可见元素 | :hidden | 所有可见元素 | :visible 

- 属性过滤选择器

选择器名称 | 语法 | 选择器名称 | 语法 
---|---|---|---|---|--- 
拥有此属性的元素 | [attribute] | 属性值为value | [attribute=value]
属性值不为value | [attribute!=value] | 属性值以value开始 | [attribute ^=value]
属性值包含value | [attribute*=value] | 属性值以value结束 | [attribute $=value]
属性值为value或为"value-" | [attribute I=value] | 选取属性用空格分割的值中包含给定的value | [attribute~=value]
满足多个条件 | [attribute1][attribute2][attribute3] |  | 

- 属性过滤选择器

选择器名称 | 语法 | 选择器名称 | 语法 
---|---|---|---|---|--- 
选取每个父元素下第index个元素(index>0) | :nth-child(index) | :nth-child(odd/even) | :nth-child(equation)
第一个元素 | :first-child | 最后一个元素 | :last-child
唯一的元素 | :only-child |  | 

- 表单对象属性过滤选择器

选择器名称 | 语法 | 选择器名称 | 语法 
---|---|---|---|---|--- 
可用元素 | :enabled | 不可用元素 | :disabled
单/复选被选中元素 | :checked | 下拉列表被选中元素 | :selected

- 表单选择器

选择器名称 | 语法 | 选择器名称 | 语法 
---|---|---|---|---|--- 
input/textarea/select/button元素 | :input | 单行文本框 | :text
密码框 | :password | 单选框 | :radio
多选框 | :checkbox | 提交按钮 | :submit
图像按钮 | :image | 重置按钮 | :reset
按钮 | :button | 上传域 | :file
不可见元素 | :hidden |  | 
