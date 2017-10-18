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
            </Directory>
            <VirtualHost *:80>
                ServerName www.study.com
                DocumentRoot 路径
            </VirtualHost>
            注:
            多IP配置方法:
                copy ifcfg-eth0 ifcfg-eth0:0
                编辑ifcfg-eth0:0,device=eth0:0

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
            
            注:httpd -l(可以看到当前是哪种模式)
                不管是Worker模式或是Prefork 模式，Apache总是试图保持一些备用的(spare)或者是空闲的子进程（空闲的服务线程池）用于迎接即将到来的请求。这样客户端就不需要在得到服务前等候子进程的产生。
            prefork:非线程,多进程
                最重要的是将MaxClients设置为一个足够大的数值以处理潜在的请求高峰，同时又不能太大，以致需要使用的内存超出物理内存的大小。
            worker:多线程,多进程
                每个进程拥有的线程数量是固定的,父进程负责子进程的建立,每个子进程可以建立ThreadsPerChild数量的的服务器线程和一个监听线程
            prefork和worker的切换:
                进入/usr/sbin目录改程序名,httpd是当前要执行的程序,httpd.*是不同模式对应的程序

    4. 仔细为apache进程分配内存
    
        * perfork
        
                <IfModule prefork.c>(有的是IfModule mpm_prefork_module)
                StartServers 5
                MinSpareServers 5
                MaxSpareServers 10
                MaxRequestWorkers 250
                MaxConnectionsPerChild 0
                </IfModule>
                
                实例说明:以服务器4G内存，采用的是prefork模式，它所应该设置的配置
                StartServers         10
                MinSpareServers      10
                MaxSpareServers      15
                ServerLimit          2000
                MaxClients           2000
                MaxRequestsPerChild  10000
                说明:
                4G内存所能够使用的HTTP连接数尽量设置小于2000
                StartServers代表启动Apache时同时启动的process数量
                MinSpareServers、MaxSpareServers代表最大与最小的备用程序数量
                MaxClients最大的同时联机数量，也就是process数量不会超过此数量,假设有10个人连上来，则Apache的程序数应有15～30个
                MaxRequestsPerChild 0
                配置每个子进程在其生存期内允许伺服的最大请求数量。到达MaxRequestsPerChild的限制后，子进程将会结束。假如 MaxRequestsPerChild为"0"，子进程将永远不会结束。将MaxRequestsPerChild配置成非零值有两个好处： 1.能够防止(偶然的)内存泄漏无限进行，从而耗尽内存。2.给进程一个有限寿命，从而有助于当服务器负载减轻的时候减少活动进程的数量。
                ServerLimi和ThreadLimit这两个指令决定了活动子进程数量和每个子进程中线程数量的硬限制。 要想改变这个硬限制必须完全停止服务器然后再启动服务器(直接重启是不行的)。

                注:
                StartServers:　　数量的服务器进程开始
                MinSpareServers:　　最小数量的服务器进程,保存备用
                MaxSpareServers:　　最大数量的服务器进程,保存备用
                MaxRequestWorkers:　　最大数量的服务器进程允许开始
                MaxConnectionsPerChild:　　最大连接数的一个服务器进程服务
                prefork 控制进程在最初建立“StartServers”个子进程后，为了满足MinSpareServers设置的需要创建一个进程，等待一秒钟，继续创建两 个，再等待一秒钟，继续创建四个……如此按指数级增加创建的进程数，最多达到每秒32个，直到满足MinSpareServers设置的值为止。这种模式 可以不必在请求到来时再产生新的进程，从而减小了系统开销以增加性能。MaxSpareServers设置了最大的空闲进程数，如果空闲进程数大于这个 值，Apache会自动kill掉一些多余进程。这个值不要设得过大，但如果设的值比MinSpareServers小，Apache会自动把其调整为 MinSpareServers+1。如果站点负载较大，可考虑同时加大MinSpareServers和MaxSpareServers。
                MaxRequestsPerChild设置的是每个子进程可处理的请求数。每个子进程在处理了“MaxRequestsPerChild”个请求后将自 动销毁。0意味着无限，即子进程永不销毁。虽然缺省设为0可以使每个子进程处理更多的请求，但如果设成非零值也有两点重要的好处：
                1、可防止意外的内存泄 漏。
                2、在服务器负载下降的时侯会自动减少子进程数。因此，可根据服务器的负载来调整这个值。MaxRequestWorkers指令集同时将服务请求的数量上的限制。任何连接尝试在MaxRequestWorkerslimit将通常被排队，最多若干基于上ListenBacklog指令。 在apache2.3.13以前的版本MaxRequestWorkers被称为MaxClients 。（MaxClients是这些指令中最为重要的一个，设定的是 Apache可以同时处理的请求，是对Apache性能影响最大的参数。其缺省值150是远远不够的，如果请求总数已达到这个值（可通过ps -ef|grep http|wc -l来确认），那么后面的请求就要排队，直到某个已处理请求完毕。这就是系统资源还剩下很多而HTTP访问却很慢的主要原因。虽然理论上这个值越大，可以 处理的请求就越多，但Apache默认的限制不能大于256。）
                
        * worker
        
                <IfModule worker.c>
                StartServers 3
                MinSpareThreads 75
                MaxSpareThreads 250 
                ThreadsPerChild 25
                MaxRequestWorkers 400
                MaxConnectionsPerChild 0
                </IfModule>
                
                <IfModule worker.c>
                StartServers         10
                MinSpareServers      10
                MaxSpareServers      15
                ServerLimit          2000
                MaxClients           2000
                MaxRequestsPerChild  10000                              
                ThreadsPerChild 25 (当使用thread来进行指定时，则说明此配置主要是为worker的模式)
                </IfModule> 
                
                注:
                StartServers:　　初始数量的服务器进程开始
                MinSpareThreads:　　最小数量的工作线程,保存备用
                MaxSpareThreads:　　最大数量的工作线程,保存备用
                ThreadsPerChild:　　固定数量的工作线程在每个服务器进程
                MaxRequestWorkers:　　最大数量的工作线程
                MaxConnectionsPerChild:　　最大连接数的一个服务器进程服务
                Worker 由主控制进程生成“StartServers”个子进程，每个子进程中包含固定的ThreadsPerChild线程数，各个线程独立地处理请求。同样， 为了不在请求到来时再生成线程，MinSpareThreads和MaxSpareThreads设置了最少和最多的空闲线程数；而MaxRequestWorkers 设置了同时连入的clients最大总数。如果现有子进程中的线程总数不能满足负载，控制进程将派生新的子进程MinSpareThreads和 MaxSpareThreads的最大缺省值分别是75和250。这两个参数对Apache的性能影响并不大，可以按照实际情况相应调节 。ThreadsPerChild是worker MPM中与性能相关最密切的指令。ThreadsPerChild的最大缺省值是64，如果负载较大，64也是不够的。这时要显式使用 ThreadLimit指令，它的最大缺省值是20000。Worker模式下所能同时处理的请求总数是由子进程总数乘以ThreadsPerChild 值决定的，应该大于等于MaxRequestWorkers。如果负载很大，现有的子进程数不能满足时，控制进程会派生新的子进程。默认最大的子进程总数是16，加大时 也需要显式声明ServerLimit（最大值是20000）。需要注意的是，如果显式声明了ServerLimit，那么它乘以 ThreadsPerChild的值必须大于等于MaxRequestWorkers，而且MaxRequestWorkers必须是ThreadsPerChild的整数倍，否则 Apache将会自动调节到一个相应值。
        
        * event
        
                <IfModule mpm_event_module>
                StartServers 3
                MinSpareThreads        25
                MaxSpareThreads       75
                ThreadLimit                 64
                ThreadsPerChild          25
                MaxRequestWorkers   30
                MaxConnectionsPerChild    1000
                </IfModule>
                <IfModule mpm_event_module>
                StartServers 3
                MinSpareThreads 75
                MaxSpareThreads 250
                ThreadsPerChild 25
                MaxRequestWorkers 400
                MaxConnectionsPerChild 0
                </IfModule> 
                
                注:
                StartServers:初始数量的服务器进程开始
                MinSpareThreads:　　最小数量的工作线程,保存备用
                MaxSpareThreads:　　最大数量的工作线程,保存备用
                ThreadsPerChild:　　固定数量的工作线程在每个服务器进程
                MaxRequestWorkers:　　最大数量的工作线程
                MaxConnectionsPerChild:　　最大连接数的一个服务器进程服务

    5. 了解自己的应用
    
            下面的命令可以列出现在加载的所有模块：
            httpd -M
            apache2ctl -M
            
    6. 压力测试
    
            ab:
            ab options hostname:port/path
            -n 在测试会话中所执行的请求个数(本次测试总共要访问的次数),默认时,仅执行一个
            -c 一次产生的请求个数(并发数),默认是一次一个
            -t 测试所进行的最大秒数,其内部隐含值是-n 50000,默认时,没有时间限制
            一般用-c和-n参数就可以了
            例:
            ab -c 5000 -n 10000 http://127.0.0.1/index.php
            这里用-c指定每次请求并发数为5000,用-n设置请求数为10000
            (如果提示:ab:Cannot use concurrency level greater than total number of requests,说明-c并发数设置得太高,ab命令本身没限制,是系统有限制)