#关于SERVER#
***

##OSI七层模型##

* 应用层

        文件传输,电子邮件,文件服务,虚拟终端等
        TFTP,HTTP,SNMP,FTP,SMTP,DNS,Telnet

* 表示层

        数据格式化,代码转换,数据加密,图片编解码等
        JPEG,MPEG,ASCII

* 会话层

        解除或建立与其他接点的联系,服务器验证用户登录断点续传等
        NFS,SQL,NetBIOS,RPC

* 传输层

        提供端对端的接口,进程,端口
        TCP,UDP

* 网络层

        为数据包选择路由,路由器,多层交换机,防火墙等
        IP,IPX,ICMP,RIP,OSPF,BGP,IGMP

* 数据链路层

        传输有地址的帧,错误检测功能,网卡,网桥,二层交换机等
        SLIP,CSLIP,PPP,ARP,RARP,MTU,帧中继,MAC,VLAN

* 物理层

        以二进制数据形式在物理媒体上传输数据,中继器,网线,集线器等
        ISO2110,IEEE802,IEEE802.2,RJ45

##TCP/IP五层模型##

* 应用层

        OSI应用层,OSI表示层,OSI会话层

* 传输屋

        OSI传输层

* 网络层

        OSI网络层
        
* 数据链路层

        OSI数据链路层

* 物理层

        OSI物理层

    >
    注:
    tcp/ip协议只关心网络层,传输层和应用层,所以下面不管是分网络接口层一层还是分数链层和物理两层,都是正确的

##TCP的三次握手##

* 客户端发送请求

        发送请求同步包SYN=1,发送客户端的请求序号seq
        (客户端端口号是大于1024的)

* 服务端应答请求并发送请求

        发送应答ACK=1,发送应答序号(客户端的序号seq+1)
        发送请求同步包SYN=1,发送服务端的请求序号seq

* 客户端确认应答并应答请求

        客户端确认服务端的应答SYN=0,看应答序号是否是客户端序号seq+1
        发送应答ACK=1,发送应答序号(服务端的序号seq+1)

* 服务端确认应答并建立连接

        服务端确认客户端的应答SYN=0,看应答序号是否是服务端序号seq+1
        连接建立

##TCP的四次挥手##

* 四次握手

        一方发送FIN(中断连接请求),另一方发送ACK(应答)
        另一方发送FIN(中断连接请求),一方发送ACK(应答)

* 为什么建立是三次,断开是四次

        因为建立的时候服务器可以SYN和ACK一起发送
        而在断开的时候,一方发送FIN,但是另一方不一定数据传送完,所以只能发ACK,然后数据传送完毕以后才发送FIN

##TCP三次握手和四次挥手的状态##

* 客户端

    - 客户端初始化一个连接
        
            发送SYN>SYN_SENT>接收SYN和ACK>
            发送ACK>ESTABLISHED
    
    - 客户端关闭一个连接

            发送FIN>FIN_WAIT_1>收到服务端ACK>FIN_WAIT_2>
            接收FIN,发送ACK>TIME_WAIT>等待30秒>CLOSED

* 服务端

        服务器应用程序创建一个侦听套接字>LISTEN>
        接收SYN>发送SYN和ACK>SYN_RCVD>接收ACK,不发送任何信息>
        ESTABLISHED>接收FIN>发送ACK>CLOSE_WAIT>
        发送FIN>LAST_ACK>接收ACK,不发送任何信息>CLOSED

##samba##

* 安装samba

        sudo apt-get install samba
        sudo apt-get install samba-client
        
* 调整Samba配置文件(匿名方式)

        1. 备份现有的配置文件
            sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
        2. 修改配置文件
            [global]
            workgroup = 工作组名称
            netbios name = 主机的netbios名称
            server string = 主机的简易说明
            security = share(share,user,domain)
                * 注:
                share:分享不需要密码,大家均可使用
                user:使用samba服务器本身的密码资料库
                domain:使用外部服务器的密码
            [winshare]
            comment = shuoming
            path = /home/phinecos/share
            browseable = yes
            guest ok = yes
            
    >    注：
        在新版本samba中，security=share无效
        需使用：
        security = user
        map to user =bad user

* 测试

        smbclient -L //localhost/winshare

* 使用

        windows下:
        \\ip或主机名\winshare

##lamp##

* 需要的软件

        httpd,mysql,mysql-server,php,php-devel,php-mysql

* httpd配置文件

        /etc/httpd/conf/httpd.conf(主要配置文件)
        /etc/httpd/conf.d/*.conf(额外配置文件)

* mysql配置文件

        /etc/my.cnf
        /var/lib/mysql(mysql资料库档案存放路径)

* php配置文件

        /etc/php.ini
        /etc/httpd/conf.d/php.cnf

* httpd.conf

        Order deny,allow(默认允许所有)
        Order allow,deny(默认拒绝所有)
        注：
            1. 最先是默认条件
            2. 然后是执行逗号前内容的对应语句
            3. 再次是执行逗号后内容的对应语句

* 虚拟目录

        原httpd.conf不动,在conf.d中增加virtual.conf
        virtual.conf中:
            <Directory "路径">
                Option FollowSymLinks
                AllowOverride None
                Order allow,deny
                allow from all
            <Directory>
            <VirtualHost *:80>
                ServerName www.study.com
                DocumentRoot 路径
            <VirtualHost>
            (
                多IP配置方法:
                    copy ifcfg-eth0 ifcfg-eth0:0
                    编辑ifcfg-eth0:0,device=eth0:0
            )

* 性能调优

    1. 使用最新版本的apache
    
            第一点就是把apache更新到最新版
            如果从源文件安装的话最好把配置文件备份以免不测
            最好使用系统自己的包管理器来更新
            例:
            yum update httpd
            aptitude safe-upgrade apache2
            
    2. 考虑升级系统内核
    
    3. 审慎选择多余处理模块MPM
    
            从Apache 2.4开始我们可以根据实际情况选择三种不同的MPM:
            n preforkMPM会开启多个进程，每个进程处理一个请求。通常我们只有在应用中使用了mod_php这样非线程安全的模块时才会使用prefork MPM。
            n workerMPM的每个进程会使用多个线程，每个线程可以处理一个请求。相比于prefork MPM它可以处理更多的并发请求。
            n eventMPM从Apache 2.4开始就成了默认的MPM模式，它与worker MPM类似每个进程也会有多个线程。不过会把KeepAlive和idle状态的连接交由一个单独的线程来处理，这样就可以腾出更多的内存来应付新的请求。eventMPM也不支持mod_php这样的非线程安全模块，好在有PHP-FPM这样的替代产品。
            
    4. 仔细为apache进程分配内存
    
            <IfModule mpm_event_module>
                StartServers 3
                MinSpareThreads        25
                MaxSpareThreads       75
                ThreadLimit                 64
                ThreadsPerChild          25
                MaxRequestWorkers   30
                MaxConnectionsPerChild    1000
            </IfModule>

    5. 了解自己的应用
    
            下面的命令可以列出现在加载的所有模块：
            httpd -M
            apache2ctl -M