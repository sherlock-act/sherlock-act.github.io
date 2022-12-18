# xpath

- XPath (XML Path Language) 是一门在 HTML\XML 文档中查找信息的语言
- 可用来在 HTML\XML 文档中对元素和属性进行遍历。

- Python中xpath如果没有选取目标节点的属性或文本的话,返回值是一个element对象

## 节点选择语法

|  表达式   |                   描述                    |
| :-------: | :---------------------------------------: |
| node name | 按照节点名称选取,节点也就是html中的标签名 |
|     /     |               从根节点选取                |
|    //     |     不考虑位置,选择所有符合条件的节点     |
|     .     |                 当前节点                  |
|    ..     |             当前节点的父节点              |
|     @     |   获取节点的属性,@后面写几点的属性名称    |
|    []     | 表示条件筛选,卸载节点后,[]中写条件表达式  |

## 条件过滤

|                   表达式                   |                             描述                             |
| :----------------------------------------: | :----------------------------------------------------------: |
|                 /ul/li[1]                  |             选取ul标签所有子标签中的第一个li标签             |
|               /ul/li[last()]               |            选取ul标签所有子标签中的最后一个li标签            |
|              /ul/li[last()-1]              |           选取ul标签所有子标签中的倒数第二个li标签           |
|           /ul/li[position()<=3]            |             选取ul标签所有子标签中的前三个li标签             |
|                //div[@lang]                |               选取所有包含了lang属性的div标签                |
|          //div[@class="cn-title"]          |              选取所有class等于cn-title的div标签              |
|          //div/book[@price>35.00]          | 选取所有div下为book的标签,并且book标签中的price属性值要大于35 |
|             //div[text()="a"]              |               选取所有标签中文本值为a的div标签               |
| //div[@class="pl"]/following-sibling::a[1] |         选取class属性为pl的div同级后面的第一个a标签          |
| //div[@class="pl"]/preceding-sibling::a[1] |         选取class属性为pl的div同级前面的第一个a标签          |

## 多条件选取

|             表达式              |                      描述                       |
| :-----------------------------: | :---------------------------------------------: |
| //li[text()=1 and @class="aaa"] |  选取所有文本值为1 且 class属性值为aaa的li标签  |
| //li[text()=1 or @class="aaa"]  | 选取所有文本值为1 或者 class属性值为aaa的li标签 |
|          //li \| //div          |              选取所有的li和div标签              |