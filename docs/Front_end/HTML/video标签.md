[返回上一页](/README.md)

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

