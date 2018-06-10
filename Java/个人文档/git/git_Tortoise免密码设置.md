## Tortoise push免密码设置
### 设置用户信息
TortoiseGit->setting->Git->'用户信息'填写用户名与邮箱
### 设置git证书存储
C:\Users\MY-PC\.gitconfig 文件中的设置证书存储
[user]
	name = xyytop
	email = xyytop@163.com
[credential]
	helper=store
### 输入登录信息
下次再输入用户名和密码会被git记住，从而在C:\Users\MY-PC目录下形成一个明文储存用户名和密码的.git-credentials文件

C:\Users\MY-PC\.git-credentials
https://admin:password@github.com
