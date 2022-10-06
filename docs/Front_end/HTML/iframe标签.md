[返回上一页](/README.md)

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
