### linux学习

```
1	查看系统版本		uname -a 		x86_64表示64位系统， i686 i386表示32位系统
2	解压缩tar		tar -xvf xxx.tar		
3	重命名		mv xxx yyy		将xxx重命名为yyy
4	设置linux服务开机自启动				
	systemctl enable nginx.service				
	查看开机自启动项目（需要翻页）				
	systemctl list-unit-files				


	linux安装node
	创建用户
1	查看系统版本下载相应node版本
2	ftp传至linux
3	解压缩
4	重命名
5	建立软连接
	sudo ln -s /home/es/nodejs/bin/npm   /usr/local/bin/
	sudo ln -s /home/es/nodejs/bin/node   /usr/local/bin/

```

linux修改文件

```
sudo vi /etc/nginx/sites-available/default
sudo nginx -s reload
退出查看
输入两次大写的Z
进入编辑模式
i
退出编辑并保持
esc  :wq
```