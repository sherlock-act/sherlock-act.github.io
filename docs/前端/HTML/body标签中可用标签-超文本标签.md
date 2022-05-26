# body标签中可用标签-超文本标签

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>超文本标签</title>
	</head>
	<body>
		<!--超链接标签：作用：实现页面的跳转功能
		                        href:控制跳转的目标位置
		                        target:_self 在自身页面打开 （默认效果也是在自身页面打开）    _blank 在空白页面打开
		-->
		<a href="https://www.baidu.com" target="_blank">点击跳转到百度</a>
		<a href="多媒体标签.html" target="_blank">点击跳转到本地多媒体标签</a>
	</body>
</html>

```

## 设置锚点

- 当一个页面太长的时候，就需要设置锚点，然后可以在同一个页面的不同位置之间进行跳转

```html
<!DOCTYPE html>
<html>
        <head>
                <meta charset="UTF-8">
                <title>设置锚点</title>
        </head>
        <body>
                <a name="1F"></a>
                <h1>手机</h1>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <p>华为p40</p>
                <a name="2F"></a>
                <h1>化妆品</h1>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <p>大宝</p>
                <a name="3F"></a>
                <h1>母婴产品</h1>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <p>奶粉</p>
                <a name="4F"></a>
                <h1>图书</h1>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <p>thinking in java</p>
                <a href="#1F">手机</a>
                <a href="#2F">化妆品</a>
                <a href="#3F">母婴产品</a>
                <a href="#4F">书籍</a>
        </body>
</html>
不同页面利用锚点：

<!DOCTYPE html>
<html>
        <head>
                <meta charset="UTF-8">
                <title></title>
        </head>
        <body>
                <a href="设置锚点.html#3F">超链接</a>
        </body>
</html>

```

