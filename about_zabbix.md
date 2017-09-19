一:监控基础

1.   自动化监控框架:

三层:  联动工具:ansible
二层:  定义管理工具:saltstack(批量管理,适合底层环境从零开始的),puppet(适合直接在现有平台开始管理)
底层:  环境预备:os(自动化装系统,PXE+kickstart)..os(cobbler)
     |
     |
  监控(监控上述服务器)
     |
  小监控(用来监控监控服务器)

2.SNMP协议:
  例:如何监控主机是否在线
    主机一(监控端)         主机二(备监控端)
                         主机三(备监控端)
    (隔一断时间发PING包)
     但是要监控主机上面的服务是否正常就需要用SNMP
     SNMP:  SERVER
            ANENT
      版本: V1 V2c V3 (1和2是明文 , V3是安全传送的但是用得少)
      主控 : SNMP SERVER
      备控 : SNMP AGENT (负责在被控节点搜集数据,
             将搜集到的数据发送给SERVER,
             可以实现对请求数据的SERVER节点进行身份验证)
     SNMP的工作过程是明文,不安全,所以可以开发专用AGENT,用于密文,如nagios,cacti
         但是,专用agent只适用于可以安装agent软件的环境,如linux,windows系统
         其它环境只能使用基于snmp的通用agent,如交换机,打印机,电话

     对于服务器系统的监控,除专用agent,如nagios,还可以使用
      基于ssh登陆到被控端执行命令或者脚本的方式
      以及通用agent

3.监控监控软件(监控软件就是把2中的内容进行整合)
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
       用zabbix代理(降低并发压力)()
     6) zabbix的组织结构
        主监控(zabbix server接收被控端发送的数据)
             (zabbix database保存数据)
             (zabbix gui展示数据)
        被控端(zabbix agent发送数据)

        zabbix监控过程逻辑图
        zabbix server
        zabbix agent
        zabbix get
        zabbix sender
     7) 相关概念
        1. 主机:就是被监控的设备或者服务器,可以是IP也可以是主机名
        2. 主机组:是主机的逻辑概念(容器)
        3. 监控项(item):指定要监控的内容
        3. 应用(application):多个item可以加入一个应用,应用就是item的组或集合
        4. 键(key):key是用来唯一标识一个监控项的关键字
        5. trigger:是一个表达式(算法),用来计算所采集到的数据是否满足触发条件
        6. event:满足触发条件以后要做的事情
        7. action:event的具体操作动作
        8. 报警升级(eccalation):
        9. 媒介(media):报警的方式类型
        10.通知(notification):报警的具体信息
        11.模版(temlate):用来快速批量监控主机的格式
        12.前端(frontend):zabbix的web接口


triger:

  triger的表达式:

    {<server>:<key>.<function>(<parameter>)}<operator><constant>
     server: host name
     key: iterm key
     function: 评估所采集的数据是否达到阈值,常用avg,sum,...
     parameter: 函数的参数,默认参数是秒
   例: key.sum(30) 将最近30秒内获取的数据求和,然后和阈值比对
       key.avg(#10) 将最近10次获取的数据进行求平平均
       min(1h,7d)

  triger的操作符:

     / + * - > < = # 
   例:
      10.0.0.224:check_cpu_load.last(0)>3
