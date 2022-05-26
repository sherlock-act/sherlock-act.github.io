# 内嵌框架iframe

- 内嵌框架就是在网页中嵌入一个网页，并让它在上一级网页中显示
- 内嵌框架使用的标签是`iframe`标签
  - `<iframe src=" URL "></iframe>`
  - URL 指定独立网页的路径
- 代码示例：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>展示图片</title>
	</head>
	<body>
		<iframe name="photo" src="图片导航.html" width="20%" height="900px"></iframe>
		<iframe name="my_iframe" src="默认展示页面.html" width="78%" height="900px"></iframe>
	</body>
</html>
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>图片导航</title>
	</head>
	<body>
		<h1>我喜欢的图片展示</h1>
		<ul>
			<li><a href="img/CHiCO with HoneyWorks.jpg" target="my_iframe" >CHICO1</a></li>
			<li><a href="img/CHiCO with HoneyWorks2.jpg" target="my_iframe">CHICO2</a></li>
			<li><a href="img/exia.jpg" target="my_iframe">exia</a></li>
			<li><a href="img/睡觉的北极狐.jpg" target="my_iframe">北极狐</a></li>
			<li><a href="img/祈-1.jpg" target="my_iframe">祈妹</a></li>
			<li><a href="img/阳光穿透加拉霍奈国家公园中的森林.jpg" target="my_iframe">森林</a></li>
		</ul>
	</body>
</html>
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title><默认展示页面/title>
	</head>
	<body>
		默认展示列表,点击图片链接显示
	</body>
</html>

```

## 框架集合

- frameset 元素可定义一个框架集
- 它被用来组织多个窗口（框架）。每个框架存有独立的文档。在其最简单的应用中，frameset 元素仅仅会规定在框架集中存在多少列或多少行。必须使用 cols 或 rows 属性。
- 框架集合：和body是并列的概念，不能将框架集合放入body中
- 代码示例

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>框架集合</title>
	</head>
	<frameset rows="20%,*,30%">
		<frame src="" >
		<frameset cols="20%,*,30%">
			<frame src="" >
			<frame src="" >
			<frame src="" >
		</frameset>
		<frameset cols="50%,*">
			<frame src="" >
			<frame src="" >
		</frameset>
	</frameset>
</html>
```

