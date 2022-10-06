# CSS概述

> CSS，全称“Cascading Style Sheets”（层叠样式表），用于设置HTML标签的样式，它的基本结构如下

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

## CSS选择器

> 所谓CSS选择器（selector）就是对HTML页面中的元素实现*一对一*，*一对多*或者*多对一*的控制，从而实现布局调整，元素类型重定义，元素美化，文本、图像美化，完善交互，控制样式过渡，播放动画等一系列的功能。

### 基础选择器

#### 标签选择器

> 权重:1
>
> 直接使用标签名选择元素

```css
div{
	width:480px;
	height:320px;
}
```

#### 类选择器

> 权重:10
>
> 根据类名选择元素

```css
.showImg{
  width:720px;
  height:480px;
}
```

#### id选择器

> 权重:100
>
> 使用id值选择元素

```css
#userName{
  position: absolute;
  top:10px;
  right:10px;
}
```

#### 后代选择器

> 后代选择器是对某元素所嵌套的指定元素进行选择，每个选择符之间用*空格*进行分割，多个嵌套层次应该以多个空格进行分割（多层嵌套难免会增加选择器带来高权重，这样在处理一些元素的特殊样式的时候会带来些困难，所以在实际开发中我们还是应该避免出现多层嵌套的后代选择器的存在）

```css
/* 后代选择器
表示某一个标签下的另一个标签
div下的所有p标签下的所有span标签
*/
div p span{
  font-size:20px;
  color:#000;
}
```

#### 子选择器

> 子选择器区别与后代选择器的地方就是，后代选择器可以选择嵌套在标签内部任意层级的标签元素，而子选择器只能选择当前标签往内一层的元素。每个选择符之间用“*>*”进行分割

```css
/* 后代选择器
表示某一个标签下的另一个标签
div下一层的p标签下一层的span标签
*/
div > p > span{
  font-size:20px;
  color:#000;
}
```

#### 伪类选择器

> 该选择器的权重值为“10”
>
> 伪类选择器和其它选择器有所不同，它是通过触发一定的“*事件*”来实现效果，也就是说如果不进行任何操作是看不到该选择器的CSS样式设置的。以Google Chrome浏览器开发者工具为例，要想看到所设置的伪类选择器样式需通过点击“ Element”标签栏下“Style”标签栏中的“*:hov*”按钮，然后勾选需要查看的操作事件进行样式查看
>
> - :hover
>
>   鼠标悬浮于该元素上设置的样式
>
> - :active
>
>   鼠标悬点击时该元素上设置的样式
>
> - :visited（不建议使用）
>
>   鼠标悬点击后该元素上设置的样式
>
> - :focus
>
>   表单元素获得焦点后设置的样式

```css
a {
  font-size: 20px;
  color: #333;
  text-decoration: none;
}
a:hover {
  background-color: #ff9;
  text-decoration: underline;
}
a: active {
  background-color:#9ff
}
```

#### 群组选择器

> 群组选择器的使用范畴是，多个选择器使用同一个样式或者同一组样式。
>
> 这在做CSS样式初始化，CSS框架设计以及后期CSS代码优化时会经常使用。
>
> 另外，群组选择器写在一起并不会叠加权重值，每个逗号之间选择器的权重值是独立计算的。

```css
div,a, input, p, .txtSpan {
  line-height: 180%;
  font-size: 20px;
  color:#393；
}
```

#### 同级元素选择器

> 该选择器能选定指定元素同级的下一个元素或同级之后匹配选择器的所有元素，它不会对权重造成影响。
>
> 配合伪类选择器经常可以做出一些很有“新意”的效果，也能减少对JavaScript的依赖。
>
> 同级元素有两种，即“*+*”和“*~*”，“+”只能选择该选择器相邻的下一个选择器，而“~”能选择该选择器后的所有同级选择器

```css
.c1:hover + .c2{
  margin-left:300px;
}
```

#### 属性选择器

> 该选择器的权重值为“10”
>
> 它所针对的既不是某个标签，也不是类名，或者ID，它是将一个标签的属性作为选择器来使用，最常用的地方就是涉及到属性多而杂的表单元素。基本写法是“*[*” + “*属性名*” + “*]*”的格式，该选择器的定义方式如下：
>
> - [属性名]{...样式设置内容...}
>
>   将标签中的一个属性作为选择选择器
>
> - [属性名="属性值"]{...样式设置内容...}
>
>   将标签中的一个属性名值对作为选择器
>
> - [type^="datetime"]{...样式设置内容...}
>
>   将标签中的一个属性名名为“type”，属性值以“datetime”开头的属性名值对作为一个选择器
>
> - [title$="picture"]{...样式设置内容...}
>
>   将标签中的一个属性名名为“title”，属性值以“picture”结束的属性名值对作为一个选择器
>
> - [title*="is"]{...样式设置内容...}
>
>   将标签中的一个属性名名为“title”，属性值含有“is”的属性名值对作为一个选择器
>
> - [title~="a"]{...样式设置内容...}
>
>   将标签中的一个属性名名为“title”，属性值含有空格分隔的词为“a”的属性名值对作为一个选择器
>
> - [title|="this"]{...样式设置内容...}
>
>   将标签中的一个属性名名为“title”，属性值等于“this”或以“this-”开头的属性名值对作为一个选择器

```css
/*所有含有for属性的元素*/
/*如：<labelfor="male">*/
[for]{width:auto;}

/*类型为密码的元素*/
/*如：<input type="password"> */
[type="password"]{width:auto;}

/*Class以code开始的全部元素*/
/* 如<span class="code1">, <span class="codetest"> */
[class^="code"]{width:auto;}

/*以.jpeg为结尾(图片格式）的所有图片元素*/
/*如：<imgsrc="img/test.jpeg">*/
[src$=".jpeg"]{width:auto;}

/*title中包含的查看”二字文本的所有元素*/
/*如：<atitle="点击查看详情"＞*/
[title*="查看"]{width:auto;}

/*title中包含“is”，且前后有空格的所有元素*/
/*如：<imgtitle="'Thisisaimage">*/
[title~="is"]{width:auto;}

/*class为“code”或以“code-”开始的元素*/
/*如：<spanclass="code">或<spanclass="code-test">*/
[class|="code"]{width:auto;}

/* 但很多时候为了避免产生歧义，我们总是会在属性选择器前方加上该元素的标签名来明确选择器的控制范围。*/
input[type="radio"], input[type= "checkbox"] {
width: auto;
}
```

