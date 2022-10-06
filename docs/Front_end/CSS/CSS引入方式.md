## CSS引用方式

> 使用样式表主要有4种方式，即，“行内样式”、“内嵌样式”、“外链样式”、“导入式”。

### 行内样式

>  是将“style”作为一个标签的属性，然后通过它的值来设置样式。写法如下

```html
<div style="width: 480px; height: 320px;"></div>
```

### 内嵌样式

> 是将样式作为个标签放置于<head>标签对以内，让浏览器在加载完成其它基本信息后，首先将样式给渲染出来。标签名为“<style>”，若项目采用的是HTML严格模式/标准模式(standard mode)开发，那需要为该标签添加一个指定MIME的属性“type”，将值设为“text/css”。写法如下：

```html
<! DOCTYPE html>
<html lang="en">
  <head>
    <metacharset="UTF-8">
      <title>css示例代码</title>
      <style>
        div
        {width: 480px;
          height: 320px;}
      </style>
      </head>
    <body>
      <div></div>
    </body>
    </html>
```

### 外链样式

> 同样是将`<link>`放置于`<head>`标签对以内，通过该标签的“href”属性的值去获取CSS文件的绝对/相对路径。该标签必须要具有“*rel*”属性，并且将值设为“*stylesheet*”,否则浏览器将不能正确的解析CSS文件进行样式渲染

- html文件中写法如下:

```html
<! DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>css示例代码</title>
    <link rel="stylesheet" href="code-3.css">
  </head>
    <body>
    <div></div>
    </body>
</html>
```

- CSS文件中写法

```CSS
@charset "utf-8";
div {
  width: 480px;
  height: 320px;
}
```

### 导入式

> 该方法是在<style>标签的内容里通过“@import”方法来导入外部CSS文件，这点和通过<link>标签导入外部样式是一样的，但其它方面却有很大不同，我们后面会讲到。这种方式的写法是：

```html
<! DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>css示例代码</title>
    <style>
      @import url("code-03.css");
    </style>
  </head>
  <body>
    <div></div>
  </body>
</html>
```

### 通过`<link>`标签引用CSS文件

> 在实际的项目开发过程中，我们一般都是将CSS单独存放在一个文件夹中，然后在HTML页面中通过`<link rel="stylesheet" href="样式表路径+名称.css">`的方式进行引用。引用后CSS文件仍然是独立的，不会受到包括HTML和JavaScript任何方法和函数的影响，如果CSS文件中涉及到文件路径的相对位置，那么也是以CSS文件所在的文件路径位置为准，而非引用它的HTML文件的文件路径位置。

> 相对于“行内样式”和“内嵌样式”而言，“外链样式”即通过<link>标签引用CSS样式有以下好处：
>
> - 简化了DOM结构，实现了内容和表现的分离，使HTML和CSS文件结构更加清晰，利于维护
> - 大大减少了CSS代码的编写量。项目越大，这一点体验得越明显
> - `<link>`可以和其它`<link>`、JS文件以及`<body>`内的内容进行多线程加载，使得加载速度更快
> - 利于项目整体风格的调整，维护起来也更加便捷。单文件修改，全网站（应用）生效
> - 浏览器会将CSS文件进行缓存，进一步地减少了加载所需时间
> - 可以根据需要利用JavaScript或Media动态的组合所需的CSS文件
> - 对搜索引擎友好，有利于SEO

## 