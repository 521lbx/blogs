### Github官网访问慢处理

操作方法：

　　打开hosts文件，可能需要管理员权限。

　　win10 hosts位置：C：\Windows\System32\drivers\etc

　　在末尾新建一行，添加如下内容：

　　# GitHub Host

　　140.82.112.26 alive.github.com

　　140.82.114.25 live.github.com

　　185.199.108.154 github.githubassets.com

　　140.82.113.22 central.github.com

　　185.199.108.133 desktop.githubusercontent.com

　　185.199.108.153 assets-cdn.github.com

　　185.199.108.133 camo.githubusercontent.com

　　185.199.108.133 github.map.fastly.net

　　199.232.69.194 github.global.ssl.fastly.net

　　140.82.112.4 gist.github.com

　　185.199.108.153 github.io

　　140.82.112.3 github.com

　　140.82.112.6 api.github.com

　　185.199.108.133 raw.githubusercontent.com

　　185.199.108.133 user-images.githubusercontent.com

　　185.199.108.133 favicons.githubusercontent.com

　　185.199.108.133 avatars5.githubusercontent.com

　　185.199.108.133 avatars4.githubusercontent.com

　　185.199.108.133 avatars3.githubusercontent.com

　　185.199.108.133 avatars2.githubusercontent.com

　　185.199.108.133 avatars1.githubusercontent.com

　　185.199.108.133 avatars0.githubusercontent.com

　　185.199.108.133 avatars.githubusercontent.com

　　140.82.113.10 codeload.github.com

　　52.217.129.177 github-cloud.s3.amazonaws.com

　　52.216.178.147 github-com.s3.amazonaws.com

　　52.216.140.12 github-production-release-asset-2e65be.s3.amazonaws.com

　　52.217.196.241 github-production-user-asset-6210df.s3.amazonaws.com

　　52.217.128.49 github-production-repository-file-5c1aeb.s3.amazonaws.com

　　185.199.108.153 githubstatus.com

　　64.71.168.201 github.community

　　185.199.108.133 media.githubusercontent.com

　　保存。

　　或者，也可以：

　　访问 http://tool.chinaz.com/dns/ ，在输入框中填写 github.com，然后点击检测按钮，会列出响应ip，如图：
    ![github](./img/github.png)

Github官网进不去怎么办？
　　在hosts文件结尾输入：

　　# github

　　52.74.223.119 github.com

　　203.208.39.99 github.com

　　打开cmd窗口

　　执行 ipconfig /flushdns

　　刷新DNS缓存

　　完成，再访问github.com就很快了。

