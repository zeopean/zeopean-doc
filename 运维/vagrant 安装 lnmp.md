
今天使用 vagrant 安装了 lnmp 包，感觉还是不错的，值得纪录一下

* 首先呢，我安装了一个 centos65 ，具体的命令是这样的
    
        vagrant box add centos65 /Users/zeopean/Downloads/mac/centos65-x86_64-20140116.box

* 接下来，我的vagrant 就装好了，需要初始化
        
        vagrant init centos65
        vagrant up

* 需要注意的是，有可能现在呢的 Vagrantfile 文件中的 config.vm.box 是用的 base,那么改了吧，改成 centos65 ，对应刚刚add时候的那个名称
    
        Vagrant.configure("2") do |config|
        config.vm.box = "hashicorp/precise32"
        end

* 紧接着，我想该进入 vagrant了
    
        vagrant ssh

* 在我们的centos65里面，存在一个 vagrant目录， 路径为： 
    ／vagrant

* 切换到里面，创建一个文件，可以看到到，里面也有个 VagrantFile ,哈哈，创建一个 vhost 目录，你退出vagrant ,来到你刚刚初始化 vagrant 到目录，你想要到效果出现了，该目录也出现了一个 vhost ， 和我们的 centos下的 ／vagrant 完全一致

* 接下来，便直接把 lnmp 把给丢了进去 ，现在，可以看看咋安装 lnmp环境了
        
    * 第一步：解压文件
        
            tar -zxvf lnmp.1.2.tar.gz 
    
    * 第二步：更新 yum ，具体原因为不知道，但是更新后，为安装得很愉快
            
            sudo yum update
    
    * 第三步，当然是到 lnmp目录里面，然后进行安装咯
        
            cd lnmp
            sudo ./install.sh lnmp

* 本来以为安装好 lnmp 就大功告成的，但是发现自己无法修改 vgrant 目录 的文件权限，导致我的站点一直无法访问，所以，还需要配置 下  config.vm.synced_folder,如下

        config.vm.synced_folder "/Users/zeopean/vgrantenv/vhost","/vagrant/vhost", create:true, :owner => "www", :group => "www", :mount_options =>["dmode=775","fmode=664"]
        #第一个目录是我本地的开发环境，第二个目录是我vbox 里面的 lnmp 目录，
        ＃owner 表示所属的用户，
        ＃group 表示所属的用户组，
        ＃dmode 表示文件夹属性，
        ＃fmode 表示文件的属性    
    
    

接下来到，就是静静到等待咯，这个过程比较就，你可以先做点其他事情，如果有不明白的地方，可以参阅这里：
        
    http://weizhifeng.net/learn-vagrant-01.html
    
    &&
    http://lnmp.org/install.html