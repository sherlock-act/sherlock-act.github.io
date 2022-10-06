[返回上一页](/README.md)

### input标签

> 输入标签
>
> - type:规定输入框的类型
>
>   - text:文本
>   - password:密码框
>   - radio:单选框
>     - 同一组单选按钮需要保证name属性值一致
>   - checkbox:多选框
>     - 同一组多选框框需要保证name属性值一致
>   - file:上传文档
>   - button: 普通按钮
>   - submit:提交按钮
>   - reset:重置按钮
>   - image:图像按钮
>     - 需要执行scr属性
>   - range:范围
>     - min:最小值
>     - max:最大值
>     - step:步长
>     - value:值
>   - date:日期
>   - week:周
>   - time:时间
>   - datetime:日期时间
>   - datetime-local:本地日期时间
>   - color:颜色
>
>   - hidden:隐藏域
>
> - name:input标签名称
>
> - value:input标签中显示的值
>
> - maxlength:字符最大长度
>
> - readonly:使表单变为只读
>
> - disabled:使表单称为禁用状态
>
> - checked:当type值为radio或checkbox的时候,标识选中状态
>
> - size:文本框课件字符显示宽度,通常使用css控制
>
> - placeholder:input中显示的提示信息

```html
<input type="text" value="" placeholder="请输入昵称"><br>
<label>密码:</label><input type="password" value="" placeholder="请输入密码"><br>
<label>邮箱:</label><input type="text" value="" placeholder="请输入邮箱">

<select name="emailType" id="emailType">
  <option value="QQ" checked>qq.com</option>
  <option value="163" checked>163.com</option>
</select>
<br>

<label>性别:</label>
<input type="radio" name="sex" checked><label>男</label>
<input type="radio" name="sex"><label>女</label>
<br>

<label>爱好:</label>
<input type="checkbox" name="like" checked><label>旅游</label>
<input type="checkbox" name="like"><label>摄影</label>
<input type="checkbox" name="like"><label>运动</label>
<br>

<p>个人简介:</p>
<textarea name="describe" id="desc" cols="30" rows="10"></textarea>
<input type="file">
<input type="submit" value="立即注册">
```

