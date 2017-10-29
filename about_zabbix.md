一:监控基础

1. 自动化运维框架:

三层:  联动工具(发现问题后可以执行后续动作):ansible
二层:  定义管理工具:saltstack(批量管理,适合底层环境从零开始的),puppet(适合直接在现有平台开始管理)
底层:  环境预备(物理环境或虚拟环境):os(自动化装系统,PXE+kickstart)..os(cobbler)
     |
  监控(监控上述服务器)
     |
  小监控(用来监控监控服务器)

2. SNMP协议:
  例:如何监控主机是否在线
    主机一(监控端)         主机二(被监控端)
                                  主机三(被监控端)
    (隔一断时间发PING包)
     但是要监控主机上面的服务是否正常就需要用SNMP
     SNMP:  SERVER
                 ANENT
      版本: V1 V2c V3 (1和2是明文 , V3是安全传送的但是用得少)
      主控 : SNMP SERVER(访问被控节点,向被控节点请求监控数据)
      被控 : SNMP AGENT (负责在被控节点搜集数据,
             将搜集到的数据发送给SERVER,
             可以实现对来请求数据的SERVER节点进行身份验证)
     SNMP的工作过程是明文,不安全,所以可以开发专用SERVER和AGENT,用于密文,如nagios,cacti
         但是,专用agent只适用于可以安装agent软件的环境,如linux,windows系统
         其它环境只能使用基于snmp的通用agent,如交换机,打印机,电话

     对于服务器系统的监控,除专用agent,如nagios,还可以使用
      基于ssh登陆到被控端执行命令或者脚本的方式
      以及通用agent

3. 监控软件(监控软件就是把2中的内容进行整合)
  1) 监控软件的功能
     获取数据
     保存数据
     显示数据
     分析数据并触发报警
   2) 常用监控软件    一般nagois和cacti配合使用
      nagios cacti zabbix
   3) cacti
      具有上面4个功能,实际上是一个保存展示的监控软件
      展示数据能力强大,保存数据能力强(rrd数据库rrdtool软件)
      报警能力差
   4) nagois
      具有4个功能,基于状态转换的监控工具,实际上是报警,
      Ok(正常状态)--准备报警状态--问题状态报警
      报警功能突出,实现短信微信报警
      保存和展示能力差,能监控的节点数量较少
      在采集数据的时候,只能同时采集,会有高并发问题,并且备控端一个进程只能发送一个指标
    5) zabbix
      功能上面就是cacti和nagois的组合体,
4. 监控目标
   所有监控范畴都可以引入到zabbix中
   设备本身做监控(IPMI设备提供的API接口)
   对OS做监控,磁盘,CPU,网络等
   对os上的服务做监控,如nginx,apache等等服务
   等等 


二 zabbix基础

  1) zabbix监控框架
          监控主机
         (监控端)(收集数据)(分析数据,触发报警--手机,邮件等)
         (展示数据)
        被监控端
         被控打印机,路由器(基于通用agent)
         被控主机一(备监控端)(基于ssh,ping,端口扫描)
         被控主机二(备监控端zabbix agent)(基于zabbix agent)
   2) zabbix的监控方式
      专用agent 常用
      通用agent
      IPMI
      PING
      端口扫描
      ssh+脚本命令,,脚本 常用
      web方式
      计算后监控
    3) 用zabbix专用agent可以监控的指标
      1. CPU
         负载,切换
      2. 内存
         使用率
         swap cache buffer
      3. 网络
        传输速率 传输错误率
      4. disk
        使用  IO
      5. 服务
        进程 port 响应时间 
      6. 日志
      7. 文件
      8.windows
    4) zabbix可用的报警方式
      1. mail
      2. sms
      3. 微信
      4. script
      5. 报警升级
     5) zabbix的分布式监控
       要监控多个机房(远程)的情况,可以用zabbix代理(降低并发压力)
        在各个机房放置一个zabbix proxy
        然后各个机房的zabbix proxy再将数据发给主监控zabbix server
     6) zabbix的组织结构和逻辑图
     
      主监控端:
      三层(zabbix gui展示数据)
      二层(zabbix database保存数据)
      底层(zabbix server接收被控端发送的数据)
            
      被控端:
      底层(zabbix agent发送数据)

       主控端:
        zabbix get(用来从被监控端的zabbix-agentd来拉取数据)
        zabbix gui(用来实现为用户展示所采信的数据,其实就是一个网站,php)
        zabbix server(从被监控端zabbix-agentd来采集数据)
        zabbix database(用来保存所采信的数据,可以是mysql,oracle等)
        (上面三个可以独立安装,也可以单独安装)
        
        被控端:
        zabbix agentd
        zabbix sender(被监控端,主动向主控端zabbix server发送数据的程序)
        
        代理端
        zabbix proxy
        
     7) 相关概念
        1. 主机:就是被监控的设备或者服务器,可以是IP也可以是主机名
        2. 主机组:是主机的逻辑概念(容器)
        3. 监控项(item):指定要监控的内容
        3. 应用(application):多个item可以加入一个应用,应用就是item的组或集合
        4. 键(key):key是用来唯一标识一个监控项的关键字
        5. trigger:是一个表达式(算法),用来计算所采集到的数据是否满足触发条件
        6. event:满足触发条件以后要做的事情
        7. action:完成event的具体实现方式(其实就是具体操作动作)
        8. 报警升级(eccalation):
        9. 媒介(media):报警的方式类型
        10.通知(notification):报警的具体信息
        11.模版(temlate):用来快速批量监控主机的格式
        12.前端(frontend):zabbix的web接口

三 zabbix安装和配置

    zabbix(不管主控机还是被控机都要安装)
    zabbix-agent(被控机安装的)
    zabbix-server
    zabbix-server-mysql
    zabbix-web
    zabbix-web-mysql

1. 安装zabbix主机端

        yum install zabbix zabbix-server zabbix-web zabbix-server-mysql zabbix-web-mysql
        
2. 安装zabbix被监控端

        yum install zabbix zabbix-agent

3. 创建mysql数据库及用户和权限

        mysql -uroot -p
        create database zabbix character utf8 collate utf8_bin;
        grant all privileges on zabbix.* to zabbix@localhost identified by 'zabbix';
        flush privileges;

4. 初始化zabbix数据库

        cd /usr/share/doc/zabbix-server-mysql-2.xxx/create
        mysql -uroot zabbix < schema.sql
        mysql -uroot zabbix < images.sql
        mysql -uroot zabbix < data.sql

5. 调整配置文件

        /etc/zabbix/zabbix_server.conf
        DBHost=localhost
        DBName=zabbix
        DBUser=zabbix
        DBPassword=zabbix
        注:
        DBHost:数据库主机
        DBName:数据库名
        DBUser:数据库用户
        DBPassword:数据库用户密码

6. 启动服务

        service zabbix-server start
        service httpd start

7. php时区设置

        /etc/httpd/conf.d/zabbix.conf(有的文章说是/etc/php.ini)
        php_value date.timezone Asia/Shanghai(有的文章说是Chongqing)

8. 使用向导设置zabbix

        数据库设置界面:设置数据库相关的信息
        zabbix server界面:是指监控主机的信息(名字可以留空)
        注:如果网页跟监控主机是分开安装的,这里就是监控主机那一台,如果安装在一台上面,就是同一台

9. 登录到zabbix

        默认的用户名和密码:Admin/zabbix
        
四. zabbix使用

1. 主界面
2. 用户和用户组
3. 主机和主机组
4. item
    key唯一表示一个内容,比如网卡:net.if.in[eth0]
    units设置一个单位,比如k,m
    use custom multiplier剩积
    update interval多少秒采集一次
    flexible interval自定义设置采集时间(上一个这一个都设置时,本选项生效)
    trends趋势图
5. graph(图形显示item的数据)
    可以把几个item的内容在一个图形中显示
6. screen(显示图形)
    可以把屏幕分割,用来显示多个图形

7. triger(触发器):
    表达式构成,定义阈值
    触发报警:
        ok>problem
        problem>ok
    triger的表达式:

    {<server>:<key>.<function>(<parameter>)}<operator><constant>
     server: host name主机名称
     key: iterm的key
     function: 评估所采集的数据是否达到阈值,常用avg,sum,...
     parameter: 函数的参数,默认参数是秒
   例: key.sum(30) 将最近30秒内获取的数据求和,然后和阈值比对
       key.avg(#10) 将最近10次获取的数据进行求平平均
       min(1h,7d) 7天以前的一个小时内的数据

  triger的操作符:

     / + * - > < = #(不等于) & | 
   例:
      {10.0.0.224:net.if.in[eth0].last(0)}>3

8. action
    实现自动报警
        1. 定义一个triger(定义针对哪个key所做的阈值)
        2. 定义一个达到阈值所要触发的动作(action
        3. 在动作中执行事件
    action:通常都是报警(通知)
        定义媒介:发送通知的途径
        定义动作:这里才是真正的动作,将消息发送到媒介
    执行的动作有两种:
        发送通知
        执行远程命令

9. 用户自定义参数userparameter(在zabbix_agentd.conf中添加)
        UserParameter=<key([参数])>,<shell command>;...;<shell command>
        可以有多个命令,但只有最后一个命令才有返回结果,返回的结果最大512K
        如:
        UserParameter=FreeMem,free -m | awk '/^Mem/{print $4}'
        UserParameter=MemInfo[*],cat /proc/meminfo | awk '/^$1/{print $$4}'
    zabbix_get -s 192.168.55.11 -k FreeMem(手工直接用的命令)
    zabbix_get -s 192.168.55.11 -k MemInfo[MemTotal] 
    item中设置:
        创建item,如
        name:FreeMem,key:FreeMem
        name:MemInfo,key:MemInfo[MemTotal]
        mysqladmin -uroot -p ping | egrep -c 'alive'
        (ping可以得到mysql在线可不在线的结果,统计一下如果在线就得到1)
    脚本的保存位置:
        默认位置(使用时可以用相对路径):
        /usr/lib/zabbix/externalscripts
        /etc/zabbix/externalscripts
        其它位置(可以改配置文件调整,但是使用时只能用绝对路径)