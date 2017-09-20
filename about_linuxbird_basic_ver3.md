#vbird
***

##零、计算机概论
## 一、linux是什么
## 二、linux如何学习
## 三、主机规划/磁碟分割
## 四、安装centos 5.x
***

## 五、首次登入与man
* date
* man
		man 待查找的名字
		man date
		(1,5,8这三个特别重要)
			1 使用者在shell环境中可以操作的指令或可执行档
			2 系统核心可呼叫的函数与工具等
			3 一些常用的函数好来屋函数库,大部分是C
			4 装置档案的说明,通常在/dev下的档案
			5 设定档或者是某些档案的格式
			6 游戏
			7 惯例与协定等,例如linux档案系统,网络协定,ascii code说明等
			8 系统管理员可用的指令
			9 跟kernel有关的文件
			NAME 简短的指令,资料名称说明
			SYNOPSIS 简短的指令下达语法简介
			DESCRIPTION 较为完整的说明,这部分仔细看
			OPTIONS 针对语法部分中,有列举的所有可用的选项说明
			COMMANDS 当这个程式在执行时,可以在此程式中下达的指令
			FILES 这个程式或资料所使用或参考或连结到的某些档案
			SEE ALSO 可以参考的,跟这个指令或资料有相关的其他说明
			EXAMPLE 一些可以参考的范例
			BUGS 是否有相关的bug
		man -f 待查找的名字
		(可查看此名字有几类说明)
		man 1-7 待查找的名字
		(打开对应类别的man手册)
		man -k man
		(查找说明档中,只要有man这个关键字就将该说明列出来)
* shutdown
		/sbin/shutdown -t 秒 -arkhncfF 时间 警告讯息
			-t 秒 过几秒后关机
			-k 不是真的关机,只是发送警告讯息出去
			-c 取消已经在进行的shutdown指令内容
			时间 这是一定要加入的参数指定系统关机的时间
		例:
		/sbin/shutdown -h 10 'i will shutdown after 10mins'
		(告诉大家,机器会在十分钟后关机)
		shutdown -h now
		(立即关机)
		shutdown -h 20:25
		(20:25关机,如超时则是明王建成20:25关机)
		shutdown -h +10
		(10分后自动关机)
		shutdown -r now
		(立即重启)
		shutdown -r +30 'the system will reboot'
		(30分后重启)
		shutdown -k now 'the system will reboot'
		(只发出警告信息)
***

##六、linux档案权限目录配置
	chgrp
		chgrp -R 目录名或文件名
			-R 递归更改
	chown
		chown -R 账号名称 档案或目录
		chown -R 账号名称:组名称 档案或目录
			-R 递归更改
	chmod
		chmod -R xyz 档案或目录
			-R 递归更改
	uname
		uname -r
	lsb_release
		lsb_release -a
***

##七、linux档案与目录管理
	目录的相关操作
		.	代表此层目录
		..	代表上一层目录
		-	代表前一个工作目录
		~	代表目前使用者身份所在的家目录
		~账号	代表账号对应的这个用户的家目录
	pwd
		pwd -P
			-P 显示真实路径,而不是连结档路径
	mkdir
		mkdir -mp 目录名称
			-m 直接设定权限,不需要看预设umask脸色
			-p 递归建立
	rmdir
	(删除空目录)
		rmdir -p 目录名称
			-p 递归删除
	$PATH
		echo $PATH
		PATH=$PATH:路径
	cp
		cp -adfilprsu 来源档 目标档
		cp options source1 source2 ... directory
			-a 等于-pdr
			-p 连同档案属性一起复制,而不是用预设值
			-d 若来源为连结档属性则复制连接档属性而非档案本身
			-r 递归复制,用于目录
			-l 建立硬连接
			-s 建立软连接
		cp -s bashrc bashrc_slink(软连接)
		cp -l bashrc bashrc_hlink(硬连接)
		cp -d bashrc_slink bashrc_slink_2
	rm
		rm -fir 档案或目录
			-f force
			-i 互动模式,删除前会提示
			-r 递归删除,常用在目录
	mv
		mv -fiu source destination
		mv options source1 source2 ... directory
	rename
	(更名)
	basename
	dirname
	(取得档案名称或目录名称)
	touch
		touch -acdmt 档案
			-a 仅更改access time
			-c 仅更改档案的时间,若档案不存在则不建立新档案
			-d 后面接欲更改的时间而不用目前的时间,也可以使用--date="日期或时间"
			-m 仅修改mtime
			-t 后面接欲更改的时间而不用目前的时间,格式为YYMMDDhhmm
	which
	(寻找执行档)
		which -a command
	whereis
	(寻找特定档案,执行档或一般档案或目录)
		whereis -bmsu 档案或目录名
			-b 只找binary格式的档案
			-m 只找在说明档manual路径下的档案
			-s 只找source来源档案
			-u 搜索不在上述三个项目当中的其他特殊档案
	locate
		locate -ir keyword
			-i 忽略大小写的差异
			-r 后面可按正则表示法的显示方法
	locate和whereis都是检索的数据库
	updatedb(更新数据库)
	find
		find path option action
***

##八、linux磁碟与档案系统
***

##九、档案与档案系统的打包
	gzip,zcat
	(gzip:可以解开compress,zip,gzip等,压缩解压都不保留源文件)
	(zcat:可以直接读取压缩包里面的文本内容)
		gzip -cdtv# 档名
		zcat 档名.gz
			-c 将压缩的资料输出到屏幕上,可透过资料流重导向来处理
			-d 解压缩的参数;
			-t 可以用来检验一个压缩档的一致性,看看档案有无错误
			-v 可以显示出原档案/压缩档案的压缩比等信息
			-# 压缩等级
		*把档案用最佳压缩比压缩,并保留原本的档案
		 gzip -9 -c man.config > man.config.gz
	bzip2,bzcat
		bzip2 -cdkzv# 档名
		bzcat 档名.bz2
			-c 将压缩的过程产生的资料输出到萤幕上
			-d 解压缩的参数
			-k 保留原始档案,而不会删除原始的档案
			-z 压缩的参数
			-v 可以显示出原档案/压缩档案的压缩比等信息
			-# 与gzip同样的,压缩比参数
	tar(打包)
		tar -j|-z cv -f 建立的档名 filename...
		tar -j|-z tv -f 建立的档名
		tar -j|-z xv -f 建立的档名 -C 目录
			-c 建立打包的档案
			-t 察看打包的档案的内容有哪些档名
			-x 解包
			-j bzip2
			-z gzip
			-v 在过程中将正在处理的档名显示出来
			-f 接要被处理的档名
			-C 在特定目录里面解包
			-p 保留资料原本的权限与属性
			-P 保留绝对路径,即允许含有根目录
			--exclude=file 在压缩过程中不要将file打包
		tar -jxv -f 打包档.tar.bz2 包中待解开的档名
		(不全部解包,只解开包中的特定文件)
		tar -jcv -f /root/system.tar.bz2 \
		--exclude=/root/etc* \
		--exclude=/root/system.tar.bz2 \
		/etc /root
		(打包不含某些档案)
		tar -jcv -f /root/abc.tar.bz2 \
		--newer-mtime="2008/09/29" /etc/*
		(打包比某个档案新的档案)
		tar -cvf - /etc | tar -xvf -
		(利用管线命令与资料流)
		(想将/etc的东西复制到一个目录,但是又不想用cp -r,就用打包的方式来进行,-表示打包的档案,但是又不想让中间档案存在)
	dump
	*当待备份的资料为单一档案系统:就可以使用完整dump功能
	*待备份的资料只是目录,并非单一档案系统:dump功能有限制
	 所有的备份资料都必需要在该目录下
	 且仅能使用level 0,亦即仅支援完整备份
	 不支援-u选项,亦即无法建立/etc/dumpdates这个时间记录档
		dump -Suvj -level -f 备份档 待备份的资料
		dump -W
			-S 仅列出后面的待备份资料需要多少磁盘空间才能够备份完
			-u 将这次dump的时间记录到/etc/dumpdates
			-v 将dump的档案过程显示出来
			-j 加入bzip2支持
			-level 等级 0,,,9 十个等级
			-f 有点类似tar,后面接产生的档案,也可以接如 /dev/st0装置档名
			-W 列出在/etc/fstab里面具有dump设定的分区是否有备份过
		例:
		dump -S /dev/hdc1
		dump -0u -f /root/boot.dump /boot
	restore
		restore -t -f dumpfile -h
		restore -C -f dumpfile -D
		restore -i -f dumpfile
		restore -r -f dumpfile
			-t 此模式用于察看dump文档有什么资料
			-C 可以将dump内的资料跟实际档案比较
			-i 进入互动模式,可以部分还原,用在目录
			-r 将整个文件系统还原的模式,用在还原档案系统的还原
			-h 察看完整备份资料中的inode与档案系统label等信息
			-f 接要处理的dump档案
			-D 与-C进行搭配,可以查出后面接的挂载点与dupm内有不同的档案
		例:

		restore -t -f /root/boot.dump
		restore -C -f /root/boot.dump
		restore -r -f /root/boot.dump(必须要到新档案系统挂载点下面去操作)
		restore -i -f /root/etc.dump(进入互动模式)
		add fil 将文件或目录加入待解压的档案列表
		delete file 将文件或目录从待解压的档案列表中移除
		extract 将待解压列表中的文件或目录解压出来
	mkisofs:建立映像档
		mkisofs -o 映像 -rv -m file 待备份档案 -V vol\
		-graft-point isodir=systemdir ...
			-o 接你想要产生的那个映像档档名
			-r 透过rock ridge产生支援unixlinux的档案资料,可记录较多的资讯
			-v 显示建立iso档案的过程
			-m 排除档案的意思同exclude
			-V 建立Volume,有点像win中看到cd title的
			-graft-point graft有转嫁或移植的意思
		例:
		mkisofs
***

##十、vim编辑器
	dos2unix
		dos2unix -kn file newfile
			-k 保留该档案原本的mtime时间格式
			-n 保留旧档,将转换后的内容输出新档
	unix2dos
		unix2dos -kn file newfile
	(dos2unix,unix2dos:转换dos与windows断行字符)
	iconv
	(转换编码集)
		iconv --list
		iconv -f 原编码 -t 新编码 filename -o newfile
***

十一、认识与学习BASH

十二、正则表示法

十三、学习shell scripts
***

##十四、linux账号管理与ACL
	初始组群
		passwd里面的GID就是初始组群,用户所属初始组,不需要在group中该组最后一栏添加该用户的用户名
	有效组群
		有效组群的作用在于新建档案后档案的初始所属组
	groups
		查看有效组群
	newgrp
	(变更有效组)
		newgrp 组名
		(将当前用户切换到另一个组的状态,是在原组状态下生成并切换到另一个组的shell环境,exit会退回到原组状态)
	useradd
	(只使用useradd增加了账号,账号处于暂时封锁状态,因为shadow中密码栏是!!)
		useradd -u UID -g 初始组群 -G 次要组群 -mM -c 说明栏 -d 家目录绝对路径 -s shell 使用者账号名
			-m 强制,要建立使用者家目录(一般账号预设值)
			-M 强制,不要建立使用者家目录(系统账号预设值)
			-r 建立一个系统账号
			-d 指定某个目录成为家目录,绝对路径
			-s 没有指定则是预设/bin/bash
			-e 账号失效日期,yyyy-mm-dd
			-f 密码是否会失效,0立即失效
			-l 为永远不失效
	useradd参考档(就是useradd的预设值)
		useradd -D
	UID,GID,密码参数预设值
		/etc/login.defs
passwd
		passwd --stdin(不加用户名,所有人都是用来更改自己的密码)
		passwd -l -u --stdin -S -n 日期 -x 日数 -w 日数 -i 日期
账号(root才能使用)
		例:echo "abc543cc" | passwd --stdin vbird2
			--stdin 可以用管道符
			-l 是lock的意思,会将shadow第二栏加上!使密码失效
			-u unlock
			-S 列出密码相关参数,就是shadow内大部分信息
			-n 多久不可修改密码
			-x 多久必须修改密码
			-w 密码过期前的警告天数
			-i 密码失效日期
	chage
	(更详细的密码参数显示功能)
		chage -ldEImMW 账号名
			-l 列出该账号详细的密码参数
			-d 日期,最近一次更改密码的日期,YYYY-MM-DD
			-E 日期,账号失效日,YYYY-MM-DD
			-I 天数,密码失效日期
			-m 天数,密码最短保留天数
			-M 天数,密码多久需要变更
			-W 天数,密码过期前警告日期
		例:
		useradd test
		echo "test" | passwd --stdin test
		chage -d 0 test
		(使用者在第一次登入时,强制他们一定要更改密码后才能够使用系统)
	usermod
	(对账号的相关信息passwd,shadow进行调整)
		usermod -cdefgGalsuLU username(用户账号)
			-c 后面接账号的说明,passwd
			-d 后面接账号的家目录,passwd
			-e 接日期,YYYY-MM-DD,shadow,账号失效日期
			-f 接天数,shadow,密码失效日期
			-g 接初始组群,passwd,GID
			-G 接次要组群,group,修改使用者能够
支援的组群(覆盖重设)
			-a 与-G合用,可增加次要群组的支援
			-l 修改账号名称,passwd
			-s 后面接实际的shell档案,/bin/bash等
			-u 后面接UID的数字
			-L 暂时将使用者的密码冻结,shadow
			-U 解禁密码,shadow
	userdel
	(删除使用者相关资料)
	(使用者相关资料有:
	passwd,shadow,group,gshadow
	/home/username,/var/spool/mail/username)
		userdel -r username
			-r 连同使用者家目录也一起删除
	finger
	(查阅很多使用者相关的资讯,大部分都是在passwd里)
		finger -s username
			-s 仅列出使用者账号全名终端代号与登入时间等等
			-m 列出与后面接的账号相同者,而不是	利用部分比对(包括全名部分)
		例:finger
		   (找出目前在系统上面登入的使用者登入时间,包括一些office officephone等个人相关信息)
	chfn
	(实际是passwd)
	(更改单finger命令显示出的电话等相关个人信息)
		chfn -foph 账号
			-f 接完整大名
			-o 办公室的房间号码
			-p 辩公室的电话号码
			-h 家里的电话号码
	chsh
	(改变shell)
		chsh -ls
			-l 列出目前系统上面可用的shell
			-s 设定修改自己的shell
		例:chsh -l
		   chsh -s /bin/csh
	id
	(查询自己或者某个用户的相关id信息)
	(这个命令可以判断系统上面是不是存在某个用户)
	groupadd
		groupadd -g gid -r 群组名称
			-g 后接特定的GID,用来直接给予GID
			-r 建立系统群组
	groupmod
		groupmod -g gid -n group_name 群组名
			-g 修改GID数字
			-n 修改群组名
	groupdel
		groupdel 群组名称
	gpasswd
		root能做的:
		gpasswd 群组名
			(不加任何参数,表示给予组一个密码)
		gpasswd -A 用户 -M 用户 组群
			-A 将组主控权交给后面的使用者管理(该群组的管理员)
			-M 将某些账号加入到这个群组中
		gpasswd -rR 组群
			-r 将组密码移除
			-R 将组密码栏失效
		组管理员能做的:
		gpasswd -ad user groupname
			-a 将使用者加入到组中
			-d 将使用者移除出组
	ACL
		启用ACL:
		文件系统参数要启用(dumpe2fs -h /dev/..)
				  (Default mount options)
		mount -o remount,acl /
		vi /etc/fstab
	setfacl
		setfacl -bkRd -m|-x acl参数 目标档名
			-m 设定后续的acl参数给档案使用
			-x 删除后续的acl参数
			(-m -x 不可以合用)
			-b 移除所有的acl设定参数
			-k 移除预设的acl参数
			-R 递归设定acl
			-d 设定预设acl参数,只对目录有效,该目录中新建的资料会引用此预设值
		例:
		setfacl -m u:vbird1:rx acl-test1
		setfacl -m u::rwx acl-test1
		(设定规范:   u:使用者账号列表:权限)
		(无使用者列表,代表设定该档案拥有者)
		setfacl -m g:mygroup1:rx act-test1
		setfacl -m m:r acl-test1
		(设定预设有效权限)
		setfacl -m d:u:myuser1:rx /srv/projuecta
		(让目录下面的所有操作都拥有此设定)
		
	getfacl
		getfacl filename
			选项几乎与setfacl相同
	su
	(身份切换指令)
	(输入被切换者密码)
	(su后面的-,有跟没有是有很大差别的,因为涉及到login-shell和non-login shell的变数读取方式)
		su -lm -c 指令 username
			- 单纯使用 - 如 su - 代表使用login-shell的变数档案读取方式来登入系统;若使用者名称没有加上去,则代表切换为root的身份
			-l 与 - 类似,但后面需要加欲切换的使用者账号,也是login-shell方式
			-m -m与-p是一样的,表示使用目前的环境设定,而不读取新使用者的设定档
			-c 仅进行一次指令,所以-c后面可以加上指令
		例:
		su(non-login shell方式变成root,环境还是原环境)
		su -(login-shell方式变成root,环境变成root环境)
		su - -c "head -n 3 /etc/shadow"(仅执行命令)
		su -l 用户名
	sudo
	(输入切换者自己的密码)
		sudo -b -u 新使用者账号
			-b 将后续的指令放到背景中让系统自行执行,而不与目前的shell产生影响
			-u 后面可以接欲切换的使用者,若无此项则代表切换身份为root
		例:
		sudo -u sshd touch /tmp/mysshd
		sudo -u vbird1 sh -c "mkdir ~vbird1/www;cd ~vbird1/www;echo 'This is index.html file' > index.html"
	visudo,sudoers
	(vi无法编辑sudoers)
		root	ALL=(ALL)	ALL
		使用者
			登入者的来源主机名称
			     可切换的身份
					可下达的指令
		%wheel	ALL=(ALL)	ALL
		(最左边加上一个%,表示后面接的是一个组群)
		%wheel 	ALL=(ALL)	NOPASSWD:ALL
		(NOPASSWD代表不需要输入密码就能使用sudo)
		myuser1 ALL=(ROOT) /usr/bin/passwd
		myuser1 ALL=(root) !/usr/bin/passwd,\
				   /usr/bin/passwd [A-Za-z]*,\
				   !/usr/bin/passwd root
		User_Alias ADMPW = pro1,pro2,myuser1,myuser2
		Cmnd_Alias ADMPWCOM = !/usr/bin/passwd,\
				   /usr/bin/passwd [A-Za-z]*,\
				   !/usr/bin/passwd root
		ADMPW	ALL=(root)	ADMPWCOM
		User_Alias ADMINS = pro1,pro2,pro3,myuser1
		ADMINS	ALL=(root)	/bin/su -
	w,who,last,lastlog
	(查询使用者)
***

十五、quota,raid,lvm
***

##十六、例行工作排程
	at(atd)
		at -mldv time
		at -c 工作号码
			-m 当at完成后即使没有输出信息,也以email通知使用者该工作已经完成
			-l 相当于atq,列出目前系统上面所有该使用者的at排程
			-d 相当于atrm,取消排程
			-v 以较明显的时间格式列出at排程中的工作
			-c 可以列出后面接的工作的实际指令内容
	crontab(crond)
		crontab -u username -l,-e,-r
			-u 只有root才能进行这个操作,给其他使用者建立移除crontab排程
			-e 编辑crontab的工作内容
			-l 查阅工作内容
			-r 移除所有工作内容,仅移除一项目,-e编辑
***

##十七、程序管理与selinux
	&(直接将指令丢到背景中执行)
		tar -zpcf /tmp/etc.tar.gz /etc &
	ctrl+z(将目前的工作丢到背景中暂停)
	jobs(观察目前的背景工作状态)
		jobs -lrs
			-l 除了列出job编号与指令串之外同时列出PID的号码
			-r 仅列出正在背景run的工作
			-s 仅列出正在背景中stop的工作
	fg(将背景工作拿到前景来处理)
		fg %jobnumber
		fg单命令取预设取出带+号的那个任务
	bg(让工作在背景下的状态变成运作中)
	kill
		kill -signal %jobnumber
		kill -l
			-l 列出目前kill能够使用的讯号有哪些
			-1 重新读取一次参数的设定档类似reload
			-2 代表与由键盘输入ctrl-c同样的动作
			-9 立刻强制删除一个工作
			-15 以正常的程序方式终止一个工作
			-SINGTERM = -15
	nohup
	(在系统背景下运行,离线不会终止)
		nohup 指令与参数 在终端机前景中工作
		nohup 指令与参数 & 在终端机背景中工作
	ps
	(建议直接背两个不同的选项)
	(ps -l只能查阅自己bash程序)
	(ps aux查阅所有系统运作的程序)
		ps aux
		ps -lA
		ps axjf
	top
	(持续侦测程序运作状态)
		top -d 数字 |top -bnp
	pstree
***

##十八、认识系统服务
***

十九、认识与分析登录档
***

##二十、开机流程、模组管理与loader
	流程
		1.BIOS
		2.MBR
		3.内核,内核加载驱动
			/boot/vmlinuz
			/boot/initrd
			/lib/modules(内核模组)
		4.init(inittab)
			/etc/init/rcS.conf->/etc/rc.d/rc.sysinit
			/etc/init/rc.conf
			...
			/etc/rc.d/rc.local
	inittab
		设定项目:run level:init的动作行为:指令项目
			1 设定项目
			  最多四个字元,代表init的主要工作项目,只是一个简单的代表说明
			2 run level
			  该项目在哪些run level下进行(35代表3和5下都执行)
			3 init的动作项目
				initdefault	代表预设的run level设定值
				sysinit		代表系统初始化的动作项目
				ctrlaltdel	代表ctrl+alt+del三个按键是否可以重新开机
				wait		代表后面栏位设定的指令项目必须要执行完毕才能结续下面其他的动作
				respawn		代表后面栏位的指令可以无限制的再生即重新生成
			4 指令项目
			  应该可以进行的指令,通常是一些script
	自定义模组
		/etc/sysconfig/modules
		/etc/modprobe.conf
	核心与核心模组
		核心
			/boot/vmlinuz或/boot/vmlinuz-version
		核心解压缩所需RAM Disk
			/boot/initrd或/boot/initrd-version
		核心模组
			/lib/modules/version/kernel或/lib/modules/$(uname -r)/kernel
		核心原始码
			/usr/src/linux或/usr/src/kernels(要安装才有,预设不安装)
		核心版本
			/proc/version
		系统核心功能
			/proc/sys/kernel
	核心模组与相依性
		/lib/modules/$(uname -r)/modules.dep
		(记录了核心模组的相依性)
		depmod -Ane
		(建立modules.dep这个文件)
			不加任何参数,是重建modules.dep内容
			-A 只有发现比modules.dep还新的模组时才更新
			-n 不写入,只是将结果输出到显示屏上
			-e 显示出目前已载入的不可执行的模组名称
	核心模组的显示
		lsmod
		(显示已经载入核心的模组)
		modinfo
		(查阅在核心内的模组,还可以检查某个模组档案)
			modinfo -adln 模组名或文件名
				-a 仅列出作者名称
				-d 仅列出该模组的说明
				-l 仅列出该模组的授权
				-n 仅列出该模组的详细路径
	核心模组的载入与移除
		insmod
		(手动载入模组)
			insmod 绝对路径完整名称 参数
		rmmod
		(手动移除模组)
			rmmod -fw 名称
				-f 强制移除不论是否使用
				-w 若正在使用,则使用完毕再移除
		modprobe
			modprobe -lcfr 名称
				-c 列出目前系统所有的模组
				-l 列出目前在/lib/modules/$(uname -r)/kernel中的所有模组完整档名
				-f 强制载入该模组
				-r 移除模组

二十一、系统设定工具
二十二、原始码与tarball
二十三、软体安装rpm与YUM
二十四、X Window设定
二十五、linux备份策略
二十六、linux核心编译与管理
