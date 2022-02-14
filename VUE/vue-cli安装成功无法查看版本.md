### vue-cli安装成功无法查看版本

#### vue无法加载文件C:\Users\Administrator\AppData\Roaming\npm\vue.ps1因为在此系统上禁止运行脚本

解决办法
1. 管理员身份运行PowerShell
2. 执行：set-ExecutionPolicy RemoteSigned
3. 输入Y，回车
4. vue -V 查看版本

