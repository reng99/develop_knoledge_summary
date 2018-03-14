## bfc解决上下外边距重叠问题

详细直接看demo:

```html
<!DOCTYPE html>
<html>
<head>
	<title>demo</title>
	<style type="text/css">
		*{
			margin:0;
			padding: 0;
		}
		#jia{
			width: 100px;
			height: 100px;
			background: red;
			margin: 20px;
		}
		#ming{
			width: 100px;
			height: 100px;
			background: blue;
			margin: 20px;
		}

	</style>
</head>
<body>
<div  style="overflow: hidden;">
	<div id='jia'></div>
</div>
		<div id='ming'></div>
</body>
</html>
```
