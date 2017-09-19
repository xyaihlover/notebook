安装:

	yum install ansible
	apt-get install ansible

	pip install ansible

准备Inventory:

	Inventory文件用来定义要管理的主机,默认位置/etc/ansible/hosts
	如果不保存在默认位置,可以通过-i选项指定

	被管理的机器可以通过IP或域名指定

	未分组的机器需保留在hosts的顶部

	分组使用[]指定,如:
	[web]
	linuxtoy.org
	
	分组也能嵌套:
	[vps:children]
	web
	db

	也可以用数字和字母来指定一系列主机,如:
	[1:3].linuxtory.org 等价于
	1.linuxtory.org 2.linuxtory.org 3.linuxtory.org
	[a:c].linuxtory.org 等价于
	a.linuxtory.org b.linuxtory.org c.linuxtory.org

小试牛刀:
	ansible -i hosts all -m ping -u www
	-i 指定inventory文件
	all 针对host文件中的所有主机执行,也可以指定组名或者模式
	-m 指定所用的模块,我们使用ansible内置的ping模块来检查能否正常管理远程机器
	-U 指定远端机器的用户
