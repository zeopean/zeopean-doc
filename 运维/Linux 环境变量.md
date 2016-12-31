
linux 环境变量

    Linux是一个多用户多任务的操作系统，可以在Linux中为不同的用户设置不同的运行环境，具体做法是设置不同用户的环境变量（称之为 Linux中定制的环境变量）。但是仍有些环境变量是用户都需要的，我们称之为Linux中常见的环境变量，本文只涉及常见的环境变量的简介！

#### Linux中常见的环境变量有：
```
    1.PATH：    指定命令的搜索路径
    2.HOME：    指定用户的主工作目录（即用户登陆到Linux系统中时，默认的目录）
    3.HISTSIZE：指保存历史命令记录的条数。
    4.LOGNAME： 指当前用户的登录名。
    5.HOSTNAME：指主机的名称，许多应用程序如果要用到主机名的话，通常是从这个环境变量中来取得的。
    6.SHELL：   指当前用户用的是哪种Shell。
    7.LANG/LANGUGE：    和语言相关的环境变量，使用多种语言的用户可以修改此环境变量。
    8.MAIL：    指当前用户的邮件存放目录。
    9.PS1：     命令基本提示符，对于root用户是#，对于普通用户是$。
    10.PS2：    附属提示符，默认是“>”。
    
    #备注：可以通过修改此环境变量来修改当前的命令符，比如下列命令会将提示符修改成字符串“Hello,My NewPrompt ”。
    　　# PS1="Hello,My NewPrompt"
    
    #注意：上述变量的名字并不固定，如HOSTNAME在某些Linux系统中可能设置成HOST
    
```

#### Linux也提供了修改和查看环境变量的命令！下面通过几个实例来说明：

    1.echo      显示某个环境变量值 echo $PATH
    2.export    设置一个新的环境变量 export HELLO="hello" (可以无引号)
    3.env       显示所有环境变量
    4.set       显示本地定义的shell变量
    5.unset     清除环境变量 unset HELLO
    6.readonly  设置只读环境变量 readonly HELLO

 



