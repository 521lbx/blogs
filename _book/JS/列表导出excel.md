### 列表导出excel
JQuery版本
```
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js"></script>
	<script>
		function download() {
			$.ajax({
				 type: "POST",
				 contentType: "application/json",
				 url: "http://192.168.1.87:8787/study/export",
				 xhrFields: {
					responseType: 'blob'
				 },
				 beforeSend: function(request) {
					request.setRequestHeader("Authorization","eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJyb2xlSWQiOiIwIiwiZGVwYXJ0bWVudElkIjoiMyIsImV4cCI6MTU3NTk3MDU2OSwidXVpZCI6IkZsdFc2QXFvcjdEUiIsInVzZXJJZCI6ImFkbWluIn0.BkmRvGl9dXFVjl-wFxHLHt92Zmqb4EbJnQG95_IF2B8");
				 },
				 data: JSON.stringify({
					columns:["studyStatus","patientName","patientSex","deviceTypeName","gg"]
				 }),
				 success: function(result) {
					let blob = new Blob([result], { type: 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet;charset=utf-8' });
					let objectUrl = window.URL.createObjectURL(blob);
					console.log(objectUrl);
					var link = document.createElement('a');
					link.href = objectUrl;
					link.download = '检查列表';
					link.click();
					window.URL.revokeObjectURL(link.href);
				 }
			 });
		}
	</script>
	<title>stomp-test</title>
</head>
<body>
<h1>stomp-test</h1>
<button onclick="download();">download</button>
</body>
</html>
```
Vue版本（<font color=#FF0000 >Vue中导出excel损坏无法打开，可能是因为项目中使用了mockjs，注释掉就好了</font>）
```
this.$http.post('/study/export', param, {
        responseType: 'blob',
    }).then(res => {
        let blob = new Blob([res], { type: 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet;charset=utf-8' });
        let objectUrl = window.URL.createObjectURL(blob);
        console.log(objectUrl);
        var link = document.createElement('a');
        link.href = objectUrl;
        link.download = '检查列表';
        link.click();
        window.URL.revokeObjectURL(link.href);
    });
```
