### js对url进行编码和解码（三种方式区别）

*** 只有 0-9[a-Z] $ - _ . + ! * ' ( ) , 以及某些保留字，才能不经过编码直接用于 URL。

***例如：搜索的中文关键字，复制网址之后再粘贴就会发现该URL已经被转码。

1、escape 和 unescape

原理：对除ASCII字母、数字、标点符号 @  *  _  +  -  .  / 以外的其他字符进行编码。

编码：escape('http://www.baidu.com?name=zhang@xiao@jie&order=1')

　　　结果："http%3A//www.baidu.com%3Fname%3Dzhang@xiao@jie%26order%3D1"

　　　escape('张')

　　　结果："%u5F20"

解码：unescape("http%3A//www.baidu.com%3Fname%3Dzhang@xiao@jie%26order%3D1")

　　　结果："http://www.baidu.com?name=zhang@xiao@jie&order=1"

　　　unescape("%u5F20")

　　　结果："张"

2、encodeURI 和 decodeURI

原理：返回编码为有效的统一资源标识符 (URI) 的字符串，不会被编码的字符：! @ # $ & * ( ) = : / ; ? + '

　　   encodeURI()是Javascript中真正用来对URL编码的函数。

编码：encodeURI('http://www.baidu.com?name=zhang@xiao@jie&order=1')

　　　结果："http://www.baidu.com?name=zhang@xiao@jie&order=1"

解码：decodeURI("http%3A//www.baidu.com%3Fname%3Dzhang@xiao@jie%26order%3D1")

　　　结果："http%3A//www.baidu.com%3Fname%3Dzhang@xiao@jie%26order%3D1"

3、encodeURIComponent 和 decodeURIComponent

原理：对URL的组成部分进行个别编码，而不用于对整个URL进行编码

编码：encodeURIComponent('http://www.baidu.com?name=zhang@xiao@jie&order=1')
　　　结果："http%3A%2F%2Fwww.baidu.com%3Fname%3Dzhang%40xiao%40jie%26order%3D1"

解码：decodeURIComponent("http%3A%2F%2Fwww.baidu.com%3Fname%3Dzhang%40xiao%40jie%26order%3D1")

　　　"http://www.baidu.com?name=zhang@xiao@jie&order=1"

