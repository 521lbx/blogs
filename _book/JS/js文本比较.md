### js文本比较(增加：蓝色  删除：红色加中删除线)

```
<!doctype html>
<html>
	<head>
		<meta charset="utf-8">
		<title>文本比较工具</title>
		<style type="text/css">
			.text textarea {
				resize: none;
				background: none repeat scroll 0 0 transparent;
				border: 0 none;
				width: 97%;
				height: 500px;
				overflow-y: scroll;
				position: absolute;
				left: 0;
				top: 0;
				z-index: 2;
				font-size: 18px;
				white-space: pre-wrap;
				word-wrap: break-word;
				word-break: break-all;
				border: 1px solid red;
			}
			.text {
				overflow-y: scroll;
				white-space: pre-wrap;
				word-wrap: break-word;
				word-break: break-all;
				width: 50%;
				float: left;
				text-align: left;
				z-index: 1;
				font-size: 18px;
				position: relative;
				min-height: 510px;
			}
			.add {
				color: blue;
			}
			.delete {
				color: red;
				text-decoration: line-through;
			}
			.button {
				width: 100%;
				line-height: 30px;
				font-size: 30px;
				border: 1px solid green;
				padding: 10px;
				cursor: pointer;
				text-align: center;
			}
			#result-box {
				padding: 20px;
				border: 1px solid blue;
			}
			.compare-box:after {
				content: "";
				display: block;
				clear: both;
			}
			#result {
				font-size: 20px;
			}
		</style>
	</head>
	<body>
		<div id="result-box">
			<pre id="result"></pre>
		</div>
		<div class="compare-box">
			<div class="text left-box">
				<textarea id="edit_textarea_1"></textarea>
			</div>
			<div class="text right-box">
				<textarea id="edit_textarea_2"></textarea>
			</div>
		</div>
		<div class="button">比较</div>
		<script type="text/javascript">
			function textchange() {
				var op = eq({
					value1: document.getElementById("edit_textarea_1").value,
					value2: document.getElementById("edit_textarea_2").value
				});
				document.getElementById("result").innerHTML = op.value2 + "\r\n";
			}
			function eq(op) {
				if(!op) {
					return op;
				}
				if(!op.eq_min) {
					op.eq_min = 3;
				}
				if(!op.eq_index) {
					op.eq_index = 5;
				}
				if(!op.value1 || !op.value2) {
					return op;
				}
				var ps = {
					v1_i: 0,
					v1_new_value: "",
					v2_i: 0,
					v2_new_value: ""
				};
				while(ps.v1_i < op.value1.length && ps.v2_i < op.value2.length) {
					if(op.value1[ps.v1_i] == op.value2[ps.v2_i]) {
						//ps.v1_new_value += op.value1[ps.v1_i].replace(/</g,"<").replace(">",">");
						ps.v2_new_value += op.value2[ps.v2_i].replace(/</g, "<").replace(">", ">");
						ps.v1_i += 1;
						ps.v2_i += 1;
						//值2增加的部分
						if(ps.v1_i >= op.value1.length) {
							ps.v2_new_value += "<span class='add'>" + op.value2.substr(ps.v2_i).replace(/</g, "<").replace(">", ">") + "</span>";
							break;
						}
						//值1删除的部分
						if(ps.v2_i >= op.value2.length) {
							//ps.v1_new_value += "<span style='" + op.value1_style + "'>值1多的" + op.value1.substr(ps.v1_i).replace(/</g,"<").replace(">",">") + "</span>";
							ps.v2_new_value += "<span class='delete'>" + op.value1.substr(ps.v1_i).replace(/</g, "<").replace(">", ">") + "</span>";
							break;
						}
					} else {
						ps.v1_index = ps.v1_i + 1;
						ps.v1_eq_length = 0;
						ps.v1_eq_max = 0;
						ps.v1_start = ps.v1_i + 1;
						while(ps.v1_index < op.value1.length) {
							if(op.value1[ps.v1_index] == op.value2[ps.v2_i + ps.v1_eq_length]) {
								ps.v1_eq_length += 1;
							} else if(ps.v1_eq_length > 0) {
								if(ps.v1_eq_max < ps.v1_eq_length) {
									ps.v1_eq_max = ps.v1_eq_length;
									ps.v1_start = ps.v1_index - ps.v1_eq_length;
								}
								ps.v1_eq_length = 0;
								break; //只寻找最近的
							}
							ps.v1_index += 1;
						}
						if(ps.v1_eq_max < ps.v1_eq_length) {
							ps.v1_eq_max = ps.v1_eq_length;
							ps.v1_start = ps.v1_index - ps.v1_eq_length;
						}

						ps.v2_index = ps.v2_i + 1;
						ps.v2_eq_length = 0;
						ps.v2_eq_max = 0;
						ps.v2_start = ps.v2_i + 1;
						while(ps.v2_index < op.value2.length) {
							if(op.value2[ps.v2_index] == op.value1[ps.v1_i + ps.v2_eq_length]) {
								ps.v2_eq_length += 1;
							} else if(ps.v2_eq_length > 0) {
								if(ps.v2_eq_max < ps.v2_eq_length) {
									ps.v2_eq_max = ps.v2_eq_length;
									ps.v2_start = ps.v2_index - ps.v2_eq_length;
								}
								ps.v1_eq_length = 0;
								break; //只寻找最近的
							}
							ps.v2_index += 1;
						}
						if(ps.v2_eq_max < ps.v2_eq_length) {
							ps.v2_eq_max = ps.v2_eq_length;
							ps.v2_start = ps.v2_index - ps.v2_eq_length;
						}
						if(ps.v1_eq_max < op.eq_min && ps.v1_start - ps.v1_i > op.eq_index) {
							ps.v1_eq_max = 0;
						}
						if(ps.v2_eq_max < op.eq_min && ps.v2_start - ps.v2_i > op.eq_index) {
							ps.v2_eq_max = 0;
						}
						if((ps.v1_eq_max == 0 && ps.v2_eq_max == 0)) {
							//两个值的字不同
							//ps.v1_new_value += "<span style='" + op.value1_style + "'>不同的" + op.value1[ps.v1_i].replace(/</g,"<").replace(">",">") + "</span>";
							ps.v2_new_value += "<span class='delete'>" + op.value1[ps.v1_i].replace(/</g, "<").replace(">", ">") + "</span>";
							ps.v2_new_value += "<span class='add'>" + op.value2[ps.v2_i].replace(/</g, "<").replace(">", ">") + "</span>";
							ps.v1_i += 1;
							ps.v2_i += 1;

							if(ps.v1_i >= op.value1.length) {
								//值2增加的部分
								ps.v2_new_value += "<span class='add'>" + op.value2.substr(ps.v2_i).replace(/</g, "<").replace(">", ">") + "</span>";
								break;
							}
							if(ps.v2_i >= op.value2.length) {
								//值1删除的部分
								//ps.v1_new_value += "<span style='" + op.value1_style + "'>值1多的" + op.value1.substr(ps.v1_i).replace(/</g,"<").replace(">",">") + "</span>";
								ps.v2_new_value += "<span class='delete'>" + op.value1.substr(ps.v1_i).replace(/</g, "<").replace(">", ">") + "</span>";
								break;
							}
							//值1删除的
						} else if(ps.v1_eq_max > ps.v2_eq_max) {
							//ps.v1_new_value += "<span style='" + op.value1_style + "'>值1删除的" + op.value1.substr(ps.v1_i, ps.v1_start - ps.v1_i).replace(/</g,"<").replace(">",">") + "</span>";
							ps.v2_new_value += "<span class='delete'>" + op.value1.substr(ps.v1_i, ps.v1_start - ps.v1_i).replace(/</g, "<").replace(">", ">") + "</span>";
							ps.v1_i = ps.v1_start;
						} else {
							//值2增加的
							ps.v2_new_value += "<span class='add'>" + op.value2.substr(ps.v2_i, ps.v2_start - ps.v2_i).replace(/</g, "<").replace(">", ">") + "</span>";
							ps.v2_i = ps.v2_start;
						}
					}
				}
				op.value1 = ps.v1_new_value;
				op.value2 = ps.v2_new_value;
				//有多个连着修改的放在一起
				var addRule = /<span class='add'>((?!<span).)+<\/span>/g;
				var deleteRule = /<span class='delete'>((?!<span).)+<\/span>/g;
				var allRule = /(<span class='delete'>((?!<span).)+<\/span><span class='add'>((?!<span).)+<\/span>){2,}/g;
				op.value2 = op.value2.replace(allRule, function(str) {
					var beforText = "",
						afterText = "";
					var beforeMatch = str.match(deleteRule);
					for(var i = 0; i < beforeMatch.length; i++) {
						var m = beforeMatch[i].match(deleteRule);
						beforText += RegExp.$1;
					}
					var afterMatch = str.match(addRule);
					for(var i = 0; i < afterMatch.length; i++) {
						var m = afterMatch[i].match(addRule);
						afterText += RegExp.$1;
					}
					return "<span class='delete'>" + beforText + "</span><span class='add'>" + afterText + "</span>";
				});
				return op;
			}
			window.onload = function() {
				document.getElementsByClassName("button")[0].addEventListener("click", textchange);
			}
		</script>
	</body>
</html>
```

