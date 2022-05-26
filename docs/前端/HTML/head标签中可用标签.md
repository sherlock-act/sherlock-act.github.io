# head标签中的内容

```html
<!DOCTYPE html>
<html>
	<!-- head标签中,一般放入页面配置信息-->
	<!-- 
		head中的标签
		meta 页面的配置信息
		link 引入外部资源
		title 页面标题
		style css样式
		script JS代码
	 
	 -->

	<head>
		<!-- 设置页面的编码,防止乱码现象
			 利用<meta>标签
			 charset="utf-8"这是属性,以键值对的形式存放 k=v
		-->
		<meta charset="utf-8" />
		
		<!-- 下面的meta标签实现的功能是,页面3秒后刷新,打开京东首页 -->
		<!-- <meta http-equiv="refresh" content="3;https://www.jd.com"> -->
		
		<!-- 页面作者 -->
		<meta name="author" content="shanlei;15308255956@163.com"/>
		
		<!-- 设置页面搜索的关键字 -->
		<meta name="keywords" content="镡磊;学习ing"/>
		
		<!-- 页面描述 -->
		<meta name="description" content="学习前端的使用"/>
		<meta name="viewport" content="width=device-width, initial-scale=1">
		
		<!-- link标签引入外部资源 -->
		<link href="https://g.csdnimg.cn/static/logo/favicon32.ico" rel="shortcut icon" type="image/x-icon">
		<!-- <title>中包裹的是页面的标题 -->
		<title>你好</title>
	</head>
	<body>
		this is a html......
	</body>
</html>
```

