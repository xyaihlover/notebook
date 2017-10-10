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
			
	>	注：
		在新版本samba中，security=share无效
		需使用：
		security = user
		map to user =bad user

* 测试

		smbclient -L //localhost/winshare

* 使用

		windows下:
		\\ip或主机名\winshare