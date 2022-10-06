# HTML结构

- 一个网页由四个部分组成
  - 文档声明部分:`<!DOCTYPE html>`
  - HTML标签:`<html></html>`
  - HEAD标签:`<heand></heand>`
    - HEAD标签中的子标签详细查看[HEAD标签设置](Front_end/HEAD标签设置.md)
  - BODY标签:`<body></body>`

```html
<!DOCTYPE html> -- 文档声明,声明这是一个html文档
<html lang="en"> -- html文档
<head>
    <meta charset="UTF-8"> 
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title> -- 网页标题
</head>
<body>
</body>
</html>
```

## body标签

> body标签是网页页面显示内容,主要有各种标签组合起来

### 标题标签

```html
<h1>level 1 title</h1>
<h2>level 2 title</h2>
<h3>level 3 title</h3>
<h4>level 4 title</h4>
<h5>level 5 title</h5>
<h6>level 6 title</h6>
```

### 段落标签

```html
<p>this is a part of content</p>
```

### 换行标签

```html
<br>
```

### 文本标签

- 粗体

```html
<strong>blod</strong>  
<b>blod</b>
<!--粗体常用的标签为strong,strong更具语义-->
```

- 斜体

```html
<i>斜体</i>
<em>斜体</em>
<cite>斜体</cite>
<!--斜体标签常用em-->
```

- 上标标签

```html
<p>(a+b)<sup>2</sup>=a<sup>2</sup>+b<sup>2</sup>+2ab</p>

```

- 下标标签

```html
<p>H<sub>2</sub>SO<sub>4</sub>指的是硫酸分子</p>￼
```

- 中划线标签

```html
<s>中划线标签</s>
```

- 下划线标签

```html
<u>下划线标签</u>
```

- 大写与小写标签

```html
<big>big word</big>
<small>small word</small>
```

- 水平线标签

```html
<hr>
```

### div标签

> div，全称“division（分区）”，用来划分一个区域。

```html
<div>
  <p></p>
  <span></span>
  <strong></strong>
</div>
```

### 特殊符号

| 特殊符号 | 说明         | 代码       |
| -------- | ------------ | ---------- |
| "        | 双引号(英文) | `&quot;`   |
| '        | 左单引号     | `&lsquo;`  |
| '        | 右单引号     | `&rsquo;`  |
| &times;  | 乘号         | `&times;`  |
| &divide; | 除号         | `&divide;` |
| >        | 大于         | `&gt;`     |
| <        | 小于         | `&lt;`     |
| &        | 与符号       | `&amp;`    |
| &mdash;  | 长破折号     | `&mdash;`  |
| \|       | 竖线         | `&#124;`   |
| 空格     | 空格         | `&nbsp;`   |
| &sect;   | 分节符       | `&sect;`   |
| &copy;   | 版权符       | `&copy;`   |
| &reg;    | 注册商标     | `&reg;`    |
| &trade;  | 商标         | `&trade;`  |
| &euro;   | 欧元         | `&euro;`   |
| &pound;  | 英镑         | `&pound;`  |
| &yen;    | 日元         | `&yen;`    |
| &deg;    | 度           | `&deg;`    |

### 有序列表标签

> 有序列表中的各个列表项是有顺序的。
>
> 有序列表从`<ol>开始，到</ol>`结束。
>
> `<ol>和</ol>标志着有序列表的开始和结束，而<li>和</li>标签表示这是一个列表项。`
>
> - reversed:规定有序列表的顺序为倒叙
>
> - start:起始值
> - type:规定有序列表的显示类型
>   - 1:默认,阿拉伯数字
>   - A:大写英文字母作为列表符号
>   - a:小写英文字母作为列表符号
>   - I:以大写罗马数字作为列表符号
>   - i:以小写罗马数字作为列表符号

```html
<ol>
  <li>html</li>
  <li>html</li>
  <li>html</li>
  <li>html</li>
</ol>
```

### 无序列表标签

> 无序列表的列表项是没有顺序的
>
> - type:控制li标签前的显示样式
>   - disc 实心圆
>   - circle 空心圆
>   - square 实心方块

```html
<ul>￼
  <li>列表项</li>￼
  <li>列表项</li>￼
  <li>列表项</li>￼
</ul>
```

### 表格标签

> -  表格：table标签
> - 表格标题: caption标签
> - 表头: th标签
> -  行：tr标签
> -  单元格：td标签

>- 合并行: rowspan
>- 合并列:colspan

```html
<table>￼
  <caption>表格标题</caption>￼
  <tr>￼
    <th>表头单元格 1</th>￼
    <th>表头单元格 2</th>￼
  </tr>￼
  <tr>￼
    <td rowspan=2>单元格 1</td>￼
    <td>单元格 2</td>￼
  </tr>￼
  <tr>￼
    <td>单元格 3</td>￼
  </tr>￼
  <tr>￼
    <td colspan=2>单元格 4</td>￼
  </tr>￼
  <tr>￼
    <td>单元格 5</td>￼
    <td>单元格 6</td>￼
  </tr>￼
</table>
```

### 图片标签

> HTML中要显示图片需要使用img标签
>
> - src:必要属性,指定图片路径
> - alt:当图片无法正常显示时的提示信息
> - title:光标停留图片上面时的提示信息
> - Width:宽度
> - height:高度

```html
<img src="../../img/demo01.png" alt="loading" title="testimage">
```

### 超链接标签

> HTML中使用a标签标识超链接
>
> - href:必要属性,指定超链接的地址引用
>   - 锚点用法,将href属指定为#+目标标签的id属性值
>   - 锚点直接返回web顶部href指定为#top
> - target:指定网页打开方式,
>   - _blank 在新窗口中打开 
>   - _self在当前窗口打开
>   - _parent在框架的父级打开
>   - _top在框架的最顶层打开
>   - iframe的name属性的值 在iframe中打开
> - download:下载 值为下载文件的名称

```html
<a href="http://www.bing.com" target="_blank">跳转至bing</a>
```

### 嵌入式框架 iframe

> 相当于web中嵌套了一个web页面
>
> - name:设置iframe的名称
> - width:设置iframe的宽度,可以设置像素或百分比
> - height:设置iframe的高度,可以设置像素或百分比
> - src:设置iframe中需要显示的页面或文件url地址
> - frameborder:是否显示边框,0或1
> - marginwidth:设置iframe内容左右侧的距离,若css设置margin属性,则本属性无效
> - marginheight:设置iframe内容上下侧的距离,若css设置margin属性,则本属性无效
> - scrolling:设置iframe是否显示滚动条,
>   - auto:默认,根据内容出现或隐藏滚动条
>   - yes:始终显示滚动条
>   - no:始终隐藏滚动条

```html
<iframe src="http://www.bing.com" frameborder="1" width="300" height="300" scrolling="auto"></iframe>
```

### 表单标签

> 表单标签通常是表单元素加提交按钮的形式出现
>
> - name:规定表单的名称
> - action:规定表单提交的地址,属性值为一个url
> - method:规定发送方式,值为get或post
> - target:规定在何处打开action中设置的url
>   - _blank 新窗口中打开
>   - _self 当前窗口打开
>   - _parent 框架的父窗口打开
>   - _top 框架的顶层窗口打开
>   - iframe的name属性值  在iframe中打开

```html
<form action="#" method="post" target="_blank">
  <label>昵称:</label><input type="text" value="" placeholder="请输入昵称"><br>
  <label>密码:</label><input type="password" value="" placeholder="请输入密码"><br>
  <label>邮箱:</label><input type="text" value="" placeholder="请输入邮箱">
  <select name="emailType" id="emailType">
    <option value="QQ" checked>qq.com</option>
    <option value="163" checked>163.com</option>
  </select><br>
  <label>性别:</label>
  <input type="radio" name="sex" checked><label>男</label>
  <input type="radio" name="sex"><label>女</label>
  <br>
  <label>爱好:</label>
  <input type="checkbox" name="like" checked><label>旅游</label>
  <input type="checkbox" name="like"><label>摄影</label>
  <input type="checkbox" name="like"><label>运动</label>
  <br>
  <p>个人简介:</p>
  <textarea name="describe" id="desc" cols="30" rows="10"></textarea>
  <p>上传个人照片:</p>
  <input type="file">
  <br>
  <hr>
  <input type="submit" value="立即注册">
</form>
```

### label标签

> 多用于表单中显示表单字段的标签

```html
<label>昵称:</label><br>
<label>密码:</label><br>
<label>邮箱:</label>
```

### input标签

> 输入标签
>
> - type:规定输入框的类型
>   - text:文本
>   - password:密码框
>   - radio:单选框
>     - 同一组单选按钮需要保证name属性值一致
>   - checkbox:多选框
>     - 同一组多选框框需要保证name属性值一致
>   - file:上传文档
>   - button: 普通按钮
>   - submit:提交按钮
>   - reset:重置按钮
>   - image:图像按钮
>     - 需要执行scr属性
>   - range:范围
>     - min:最小值
>     - max:最大值
>     - step:步长
>     - value:值
>   - date:日期
>   - week:周
>   - time:时间
>   - datetime:日期时间
>   - datetime-local:本地日期时间
>   - color:颜色
>   
>   - hidden:隐藏域
>   
> - name:input标签名称
>
> - value:input标签中显示的值
>
> - maxlength:字符最大长度
>
> - readonly:使表单变为只读
>
> - disabled:使表单称为禁用状态
>
> - checked:当type值为radio或checkbox的时候,标识选中状态
>
> - size:文本框课件字符显示宽度,通常使用css控制
>
> - placeholder:input中显示的提示信息

```html
<input type="text" value="" placeholder="请输入昵称"><br>
<label>密码:</label><input type="password" value="" placeholder="请输入密码"><br>
<label>邮箱:</label><input type="text" value="" placeholder="请输入邮箱">

<select name="emailType" id="emailType">
  <option value="QQ" checked>qq.com</option>
  <option value="163" checked>163.com</option>
</select>
<br>

<label>性别:</label>
<input type="radio" name="sex" checked><label>男</label>
<input type="radio" name="sex"><label>女</label>
<br>

<label>爱好:</label>
<input type="checkbox" name="like" checked><label>旅游</label>
<input type="checkbox" name="like"><label>摄影</label>
<input type="checkbox" name="like"><label>运动</label>
<br>

<p>个人简介:</p>
<textarea name="describe" id="desc" cols="30" rows="10"></textarea>
<input type="file">
<input type="submit" value="立即注册">
```

### 文本域标签 textarea

> 可以理解为长文本标签
>
> - rows:文本的行数
> - cols:文本的列数

### 下拉框select标签

> 通过`<select>`标签可以创建单选和多选的下拉菜单
>
> `<option>`是它必须得子标签,否则将不能通过任何可选项
>
> `<option>`标签通常需要一个value属性,用来在数据操作时准确通过该属性值到对应标签的内容
>
> `multiple`参数用来控制select标签是否可以进行多项选择
>
> selected属性用来控制选中状态,或者写成checked

```html
<select name="emailType" id="emailType">
  <option value="QQ" checked>qq.com</option>
  <option value="163" checked>163.com</option>
</select>

<select multiple="multiple">
  <opthon value="0" selected="selected">frank</opthon>
  <opthon value="1">tank</opthon>
  <opthon value="2">joy</opthon>
  <opthon value="3">dog</opthon>
  <opthon value="4">geek</opthon>
  <opthon value="5">rose</opthon>
  <opthon value="6">jeck</opthon>
</select>
```

- 分组下拉菜单

```html
<select>
    <optgroup label="食品">
        <option value="0">干脆面</option>
        <option value="1">米线</option>
        <option value="2">火锅</option>
    </optgroup>
    <optgroup label="电器">
        <option value="3">PS5</option>
        <option value="4">电视</option>
        <option value="5">投影仪</option>
    </optgroup>
    <optgroup label="厨房用品">
        <option value="6">筷子</option>
        <option value="7">菜刀</option>
        <option value="8">饭碗</option>
    </optgroup>
</select>
```

### 按钮标签button

> button标签是按钮元素
>
> - type属性
>   - button
>   - submit
>   - reset

```html
<form action="" name="testForm">
    <button type="button">普通按钮</button>
    <button type="submit">提交按钮</button>
    <button type="reset">重置按钮</button>
</form>
```

### output标签

> output标签可以用来显示不同类型的输出
>
> - for:需要显示的目标标签的id值

```html
<form oninput="result.value=parseInt(rangeVal.value)">
    <label>0</label>
    <input type="range" name="range" id="rangeVal" min="0" max="100" value="30">
    <label>100</label>
    <label>你的选择</label>
    <output name="result" for="rangeVal"></output>
</form>
```

### mark标签

> 像荧光笔一样突出标记中的文本

```html
<p>这是一段文本,通过<mark>mark</mark>>标签突出重点</p>
```

### meter标签

> 用于度量属性“value”的值的一个标签，通过判断“value”的值是否在一个合适的区间，从而显示出不同级别颜色。如果值在*合理区间*会显示成一个值内容比例为“绿色”的横条，如果值在*不合理区间*会显示成一个值内容比例为“红色”的横条，而鉴于两者之间则显示为“黄色”的横条。
>
> - max:最大值
> - min:最小值
> - high:规定高范围的度量值,超过low和high值区间后显示黄色
> - low:规定地范围的度量值,超过low和high值区间后显示黄色
> - optimum:规定最佳的度量值
> - value:值,可以使用0-1的浮点值

```html
<section>
    <p>
        <meter value="5" max="10" min="0" low="3" high="7"></meter>
    </p>
    <p>
        <meter value="0.9" max="1" min="0" low="0.3" high="0.7"></meter>
    </p>
</section>
```

### progress标签

> 用于显示进度信息的标签
>
> - max:最大值的取值
> - value:显示值
> - value与max配合达到现实进度百分比效果

```html
<progress max="100" value="50"></progress>
```

### audio标签

> 在页面中加载音频,目前HTML5标准中,本标签主要支持三种格式的音频文件,分别是`ogg`,`mp3`,`wav`格式
>
> - autoplay:自动播放,取值范围:autoplay
> - controls:是否向用户显示控件,取值范围:controls
> - loop:是否循环播放,取值范围:loop
> - muted:是否静音,取值范围:muted
> - preload:是否在页面加载的时候就进行加载,
>   - 取值范围:
>     - auto:当页面加载后加载整个音频
>     - metadata:页面加载后只载入元数据
>     - none:页面加载后不再入音频
> - src:音频的url地址

```html
<audio controls="controls" preload="auto" autoplay="autoplay">
    <source src="/Users/yy/Music/酷狗音乐/BQ/111.mp3" type="audio/mpeg">
    <source src="/Users/yy/Music/酷狗音乐/BQ/111.ogg" type="audio/ogg">
</audio>
```

### video标签

> 在页面中加载视频文件,目前HTML5标准中,本标签主要支持三种格式的音频文件,分别是`ogg`,`mp4`,`webm`格式
>
> - width:播放器的宽度
> - height:播放器的高度
> - autoplay:自动播放,取值范围:autoplay
> - controls:显示控件,取值范围:controls
> - loop:循环播放,取值范围:loop
> - preload:是否在页面加载的时候就进行加载,
>   - 取值范围:
>     - auto:当页面加载后加载整个音频
>     - metadata:页面加载后只载入元数据
>     - none:页面加载后不再入音频
> - src:音频的url地址

```html
<video height="320" width="480" controls="controls" preload="auto">
    <source src="./1.mp4" type="video/mp4">
</video>
```

## html全局属性

### 唯一标识符"id"

> 该属性能用于所有的HTML元素，为HTML元素指定一个唯一的标识符，用于CSS设置，JavaScript进行操作或其它脚本语言及服务器端语言进行设置操作

```html
<div id="d1">
  一个div
</div>
```

### 元素类名"class"

> 该属性可以用于所有HTML元素，为元素添加一个或*多个*类名。通常是用于CSS设置或配合JavaScript进行操作设置，多个类名以空格符进行分隔。
>
> 一个元素的class属性值可以是多个

```html
<div class="c1">
  一个div
</div>

<!-- 多个class属性值 -->
<div class="c1 c2">
  一个div
</div>
```

### tab键切换顺序tabindex

> 该属性用于设定当用户按下键盘上的“Tab”键后，页面内可以获得焦点的元素获得焦点的次序（默认是基于文档流“从左到右，从上到下”的次序）。切换次序的先后遵循以下规则：
>
> - 必须为正整数
> - 数字小的先获得焦点，数字大的后获得焦点
> - 数字并不需要连续，如“1、2、5、7...”也能正常按次序跳转焦点
> - 同样的数字，在文档流中先出现的先获得焦点，后出现的后获得焦点
> - 不能为负数，否则会被忽略
> - 可以为“0”，但会被排序到最后一个获得焦点

### 改变文字的方向dir

> 该属性可以设置元素内文本的方向，它包含两个值：
>
> - ltr
>
>   默认，文本从左往右显示。
>
> - rtl
>
>   文本从右往左显示。

### 用户私有数据定制"data-"

> 该属性本身并不会对元素及相关联的元素造成任何影响，也就是说该属性会被浏览器用户代理忽略。属性“data-*”后面的“*”号可以是用户自定义的英文单词、数字、横线“-”和下划线“_”等*字符串*。如：“data-username”、“data-photo_1”、“data-list-item_01”等。
>
> 该属性可以有属性值，也可以没有属性值，而属性值也完全是用户自定义的字符串。
>
> 该属性的作用和“class”属性的作用比较相似（但该属性不被较老版本的浏览器支持），同样可以通过它去进行CSS样式的设置，也可以被JavaScript代码进行DOM操作，数据获取、设置等，但很多时候“class”中的值是用于CSS样式设置的，如果对其操作修改会造成自身样式或后代元素的样式错乱，这个时候通过去操作开发者自定义“data-*”属性更为稳妥，也更为规范。
