### 移动端copy
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		 <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
		<title></title>
		<style>
			greeting{
				color: red;
				display: block;
			}
		</style>
		<script type="text/javascript" src="js/jquery-2.1.0.js" ></script>
	</head>
	<body>
		<div id="" onclick="img()">
			点击复制
		</div>
		<input readOnly="true" style="outline: none;border: 0px; color: rgba(0,0,0,0.0);position: absolute;left:-200px; background-color: transparent" id="biao1" value="要复制的sdf内容"/>
		<div id="biaoios" style=";position: absolute;left:-200px; color: rgba(0,0,0,0);background-color: transparent" >要复制的内容ssss</div>
		<script>
			function img()
			{
				if (navigator.userAgent.match(/(iPhone|iPod|iPad);?/i)) {//区分iPhone设备
					window.getSelection().removeAllRanges();//这段代码必须放在前面否则无效
					var Url2=document.getElementById("biaoios");//要复制文字的节点
					var range = document.createRange();
					// 选中需要复制的节点
					range.selectNode(Url2);
					// 执行选中元素
					window.getSelection().addRange(range);
					// 执行 copy 操作
					var successful = document.execCommand('copy');
 
					// 移除选中的元素
					window.getSelection().removeAllRanges();
				}else{
					var Url2=document.getElementById("biao1");//要复制文字的节点
					Url2.select(); // 选择对象
					document.execCommand("Copy"); // 执行浏览器复制命令
				}
			}
//			$("#biao1").val("要复制的内容");//要复制的内容
//			document.getElementById("biaoios").innerHTML='要复制的内容'+"";
//			img();
		</script>
	</body>
</html>

```

