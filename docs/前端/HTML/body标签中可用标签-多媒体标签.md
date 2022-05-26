# body标签中可用标签-多媒体标签

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>多媒体标签</title>
	</head>
	<body>
		<!--图片
		                        src:引入图片的位置
		                                引入本地资源
		                                引入网络资源
		                        width:设置宽度
		                        height:设置高度
		                        注意:一般高度和宽度只设置一个即可，另一个会按照比例自动适应
		                        title:鼠标悬浮在图片上的时候的提示语，默认情况下（没有设置alt属性） 图片如果加载失败那么提示语也是title的内容
		                        alt:图片加载失败的提示语
		                -->
        <!-- 图片 -->
		<img src="./img/226556.png" width="300px">
		<br>
		<!-- 音频 -->
		<embed src="audio/douoble_dragon.mp3"></embed>
		<br>
		<!-- 视频 -->
		<embed src="video/山南机房改参数压缩版.mp4"></embed>
	</body>
</html>
```

