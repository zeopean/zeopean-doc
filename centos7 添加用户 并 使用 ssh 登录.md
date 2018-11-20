## centos7 添加用户 并 使用 ssh 登录

1.创建账号

```

adduser admin           	//添加一个新用户，名字叫admin
passwd admin            	//设置用户密码
gpasswd -a sirius wheel  	//给予sudo权限, 当权限不够时，可以用sudo
lid -g wheel             	//查询所有带sudo权限的用户


```

2.给 admin 添加 sudo 权限

```

chmod -v u+w /etc/sudoers

vim /etc/sudoers
-- 在 sudoers 添加 admin ALL=(ALL) ALL

chmod -v u-w /etc/sudoers


```


3.新用户使用 ssh 的 rsa 对登录

```
在 /home/admin/.ssh 目录添加 authorized_keys, 并把 用户 在 本地电脑的 key 放上去

```

4.配置 ssh_config

```
SSH设置保存在 /etc/ssh/sshd_config

PermitRootLogin no //阻止root用户登陆 
AllowUsers admin  //允许制定用户使用SSH登陆
PasswordAuthentication no //阻止用户密码SSH登陆

```