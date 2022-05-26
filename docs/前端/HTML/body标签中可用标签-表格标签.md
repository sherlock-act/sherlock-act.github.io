# body标签中可用标签-表格标签

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>表格标签</title>
	</head>
	<body>
		<!--表格：4行4列
		                        table:表格
		                        tr:行
		                        td:单元格
		                        th:特殊单元格：表头效果：加粗，居中
		                        默认情况下表格是没有边框的，通过属性来增加表框：
		                        border:设置边框大小
		                        cellspacing：设置单元格和边框之间的空隙
		                        align="center"  设置居中
		                        background 设置背景图片 background="img/ss.jpg"
		                        bgcolor :设置背景颜色
		                        rowspan:行合并
		                        colspan：列合并
		-->
		<table border="1px" cellspacing="0px" bgcolor="cyan" align="center">
			<tr bgcolor="green">
				<td>学号</td>
				<td>姓名</td>
				<td>年龄</td>
				<td>成绩</td>
			</tr>
			<tr>
				<td>7514</td>
				<td>丽丽</td>
				<td>18</td>
				<td rowspan="3">99</td>
			</tr>
			<tr>
				<td colspan="2">7515</td>
				
				<td>20</td>

			</tr>
			<tr>
				<td>7516</td>
				<td>菲菲</td>
				<td>21</td>

			</tr>
		</table>
	</body>
</html>

```

