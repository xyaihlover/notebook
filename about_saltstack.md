saltstack

(saltstack适合从零开始的平台,puppet适合从现有平台开始)

epel源:
服务器端:yum install salt-master
客户端:yum install salt-minion

服务端:配置/etc/salt/master
客户端:配置/etc/salt/minion

salt-key -L
salt	选项	对象	命令	例
salt -E "正则表达式" test.ping	salt -E "^ln.*" test.ping
salt -L 包含对象的列表 test.ping	salt -L "lamp,lnamp" test.ping
salt -G
	salt ‘CMN-NC-3-3O1′ grains.ls
	salt -G 'os:CentOS' test.ping
	salt -G 'cpuarch:x86_64' grains.item num_cpus
salt -N 这个参数是基于组来弄的 前提是得先分好组
	在服务器配置文件 添加分组
salt -E "^ln" cmd.run "hostname"
