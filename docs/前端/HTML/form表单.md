# form表单

- 表单在 Web 网页中用来给访问者填写信息，从而能采集客户端信息，使网页具有交互的功能

- 一般是将表单设计在一个Html 文档中，当用户填写完信息后做提交(submit)操作

- 一个表单一般应该包含用户填写信息的输入框,提交按钮等，这些输入框,按钮叫做控件,表单很像容器,它能够容纳各种各样的控件

- ```html
  <form action＝"url" method="get|post" name="myform" ></form>
  -name：表单提交时的名称
  -action：提交到的地址
  -method：提交方式，有get和post两种，默认为get
  ```

- 表单与表单元素代码示例如下

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>表单元素</title>
	</head>
	<body>
		<form action="" method="get">
			<!--表单元素-->
            <!--文本框:
                input标签使用很广泛，通过type属性的不同值，来表现不同的形态。
                type="text"  文本框，里面文字可见
                表单元素必须有一个属性：name 有了name才可以提交数据,才可以采集数据
                然后提交的时候会以键值对的形式拼到一起。
                value:就是文本框中的具体内容
                键值对：name=value的形式
                如果value提前写好，那么默认效果就是value中内容。
                一般默认提示语：用placeholder属性，不会用value--》value只是文本框中的值。

                readonly只读：只是不能修改，但是其他操作都可以，可以正常提交
                disabled禁用：完全不用，不能正常提交

                写法：
                readonly="readonly"
                readonly
                readonly = "true"
			 -->
			 <!-- 文本框 -->
			<input type="text" name="user" id="user" value="" placeholder="请录入账号" />
			<input type="text" name="user2" id="user2" value="123123" readonly="readonly" />
			<input type="text" name="user3" id="user3" value="456456" disabled="disabled" />
			<!-- 密码框 -->
			<input type="password" name="password" id="password" value="" placeholder="请输入密码"/>
			
			<!-- 单选按钮 -->
			<!--单选按钮：
                注意：一组单选按钮，必须通过name属性来控制，让它们在一个分组中，然后在一个分组里只能选择一个
                正常状态下，提交数据为：gender=on ，后台不能区分你提交的数据
                不同的选项的value值要控制为不同，这样后台接收就可以区分了

                默认选中：checked="checked"
            -->
			<input type="radio" name="gender" id="gender" value="1" checked="checked"/>男
			<input type="radio" name="gender" id="gender" value="0" />女
			
			<!-- 多选按钮 -->
            <!--多选按钮:
                必须通过name属性来控制，让它们在一个分组中，然后在一个分组里可以选择多个
                不同的选项的value值要控制为不同，这样后台接收就可以区分了
                多个选项提交的时候，键值对用&符号进行拼接：例如下：
                favlan=1&favlan=3
            -->
			喜欢的语言：
			<input type="checkbox" name="lan" id="lan" value="java" checked="checked"/>java
			<input type="checkbox" name="lan" id="lan" value="python" checked="checked"/>python
			<input type="checkbox" name="lan" id="lan" value="C++" />C++
			<input type="checkbox" name="lan" id="lan" value="golang" />golang
			<input type="checkbox" name="lan" id="lan" value="C#" />C#
			
			<!-- 文件 -->
			<input type="file" />
			
			<!-- 隐藏域 -->
			<input type="hidden" name="user6" id="" value="123" />
			<input type="hidden" name="user7" id="" value="456" />
			<input type="hidden" name="user8" id="" value="789" />
			
			<!-- 普通anniu -->
			<!--普通按钮：普通按钮没有什么效果，就是可以点击，结合JS使用，可以加入事件-->
			<input type="button" name="button" id="" value="button" />
			
			<!--特殊按钮：重置按钮将页面恢复到初始状态-->
			<input type="reset" />
			
			<!--特殊按钮：图片按钮-->
			<input type="image" src="img/exia.jpg" style="width: 30%; height: 30%;"/>
			
			<!-- 下拉列表 -->
			<!--下拉列表
			                                默认选中：selected="selected"
			                                多选：multiple="multiple"
			                        -->
			喜欢的城市：
			<select name="city" multiple="multiple">
				<option value="0">---请选择---</option>
				<option value="1" selected="selected">成都</option>
				<option value="2">西安</option>
				<option value="3">德阳</option>
				<option value="4">北京</option>
				<option value="5">上海</option>
			</select>
			
			<!-- 多行文本框 -->
			自我介绍
			<textarea rows="10" cols="" style="resize: none;">
				请在这里填写信息
			</textarea>
			
			<!-- label标签 -->
			<!--label标签
				一般会在想要获得焦点的标签上加入一个id属性，然后label中的for属性跟id配合使用。
			                        -->
			<label for="uname">用户名：</label><input type="text" name="uname" id="uname" value="" />
            
            <!-- email -->
			<input type="email" name="email" id="" value="" />
			<!-- url -->
			<input type="url" name="url" id="" value="" />
			<!-- color -->
			<input type="color" name="color" id="" value="" />
			<!-- number -->
			<input type="number" name="number" max="10" min="1" step="2"/>
			<!-- range -->
			<input type="range" name="range" min="1" max="10" />
			<!-- date -->
			<input type="date" name="date" id="" value="" />
			<!-- month -->
			<input type="month">
			<!-- week -->
			<input type="week" name="week" />
			<input type="submit" />
			<br>
			<br>
			<br>
			<!--
                HTML5新增属性：
                multiple：多选
                placehoder:默认提示
                autofocus:自动获取焦点
                required:必填项
            -->
			<input type="text" autofocus="autofocus" required="required"/>
			
			<!-- 特殊按钮，提交按钮，具备提交功能 -->
			<input type="submit"/>
		</form>
	</body>
</html>

```

