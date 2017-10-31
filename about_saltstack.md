#saltstack#
***

*凌阳zabbix视频教程中说:
(saltstack适合从零开始的平台,puppet适合从现有平台开始)*

##安装##

    1.安装epel源
    2.安装saltstack
        服务器端:yum install salt-master
        客户端:yum install salt-minion

##配置##

    服务端:配置/etc/salt/master
        修改interface(设成服务端)
    客户端:配置/etc/salt/minion
        修改master(设成服务端)

##认证##

    salt-key -L(显示当前key的状态)
        Accepted Keys为被服务端接受的KEY
        Denied Keys为被服务端阻止的KEY
        Unaccepted Key未被服务端接受的KEY
        Rejected Keys为被服务端拒绝的KEY
    salt-key常用命令:
        -a ACCEPT --accept=ACCEPT 接受给出的KEY
        -A --accept-all 接受所有KEY
        -r --reject=
        -R --reject-all
        -d --delete=
        -D --delete-all

##使用##
salt    选项    对象    命令    例
salt -E "正则表达式" test.ping    salt -E "^ln.*" test.ping
salt -L 包含对象的列表 test.ping    salt -L "lamp,lnamp" test.ping
salt -G
    salt ‘CMN-NC-3-3O1′ grains.ls
    salt -G 'os:CentOS' test.ping
    salt -G 'cpuarch:x86_64' grains.item num_cpus
salt -N 这个参数是基于组来弄的 前提是得先分好组
    在服务器配置文件 添加分组
salt -E "^ln" cmd.run "hostname"