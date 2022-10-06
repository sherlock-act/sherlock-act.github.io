[返回上一页](/README.md)

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

