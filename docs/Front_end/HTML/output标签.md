[返回上一页](/README.md)

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

