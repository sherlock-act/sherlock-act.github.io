[返回上一页](/README.md)

### meter标签

> 用于度量属性“value”的值的一个标签，通过判断“value”的值是否在一个合适的区间，从而显示出不同级别颜色。如果值在*合理区间*会显示成一个值内容比例为“绿色”的横条，如果值在*不合理区间*会显示成一个值内容比例为“红色”的横条，而鉴于两者之间则显示为“黄色”的横条。
>
> - max:最大值
> - min:最小值
> - high:规定高范围的度量值,超过low和high值区间后显示黄色
> - low:规定地范围的度量值,超过low和high值区间后显示黄色
> - optimum:规定最佳的度量值
> - value:值,可以使用0-1的浮点值

```html
<section>
    <p>
        <meter value="5" max="10" min="0" low="3" high="7"></meter>
    </p>
    <p>
        <meter value="0.9" max="1" min="0" low="0.3" high="0.7"></meter>
    </p>
</section>
```

