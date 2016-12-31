**centos 安装subversion**

(参考：http://blog.feehi.com/linux/252.html)

* 下载最新版subversion       

    wget http://mirror.bit.edu.cn/apache/subversion/subversion-1.9.3.tar.gz

* 解压并进入          
    
        tar -xvzf subversion-1.9.3.tar.gz
        
        cd subversion-1.8.11

* 安装apr-util         

       yum install apr-util apr-util-devel


* 安装sqlite     

       yum install sqlite sqlite-devel
       
* 如果yum sqlite 后，仍然不行，则会显示以下错误
    
    ![image](http://images2015.cnblogs.com/blog/631777/201604/631777-20160415102351441-605330114.jpg)
这个时候，只用 通过获取 amakgamation 
    
    wget http://www.sqlite.org/sqlite-amalgamation-3071501.zip
    

通过命令进行解压，然后重命名
    
    unzip sqlite-amalgamation-3071501.zip
    mv sqlite-amalgamation-3071501 sqlite-amalgamation

* 运行configure脚本  

        /configure –prefix=/usr/local/subversion  


* 编译并安装       
 
       make && make install

* 安装完成后，我们来进行配置
    
    *  创建版本目录
        
        mkdir /var/svn
      
    * 插件版本库 
        
        svnadmin create svn/repo

    * 配置文件的使用
        
        * 配置 authz
            
            zeopean= zeopean

            [repo:/]
            @zeopean = rw

        * 配置 passwd

            zeopean = password

        
        * 配置 svnserve.conf
            
            [general]
            anon-access = none
            auth-access = write
            password-db = passwd
            authz-db = authz
            
* 配置完成后，重启吧
        
    svnserve -r -d /var/svn

* 然后使用客户端 进行检出
    
    svn://ip-addr/svn 



        
        
