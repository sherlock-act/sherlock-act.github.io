# body标签中可用标签-列表标签

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>列表标签</title>
	</head>
	<body>
		<!--无序列表:
		                        type:可以设置列表前图标的样式   type="square"
		                        如果想要更换图标样式，需要借助css技术： style="list-style:url(img/act.jpg) ;"
		-->
		<h1>无序列表标签</h1>
		<ul type="square">
			<li>java</li>
			<li>C++</li>
			<li>python</li>
			<li>golang</li>
			<li>mysql</li>
			<li>oracle</li>
			<li>redis</li>
		</ul>
		
		<!--有序列表:
		                        type:可以设置列表的标号：1,a,A,i,I
		                        start:设置起始标号
		-->
		<h1>有序列表标签</h1>
		<ol type="A" start="2">
			<li>起床</li>
			<li>洗漱</li>
			<li>上班</li>
			<li>午休</li>
			<li>下班</li>
		</ol>
	</body>
</html>
```

