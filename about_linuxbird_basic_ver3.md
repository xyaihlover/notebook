***�㡢���������
***һ��linux��ʲô
***����linux���ѧϰ
***���������滮/�ŵ��ָ�
***�ġ���װcentos 5.x
***�塢�״ε�����man
	date
	man
		man �����ҵ�����
		man date
		(1,5,8�������ر���Ҫ)
			1 ʹ������shell�����п��Բ�����ָ����ִ�е�
			2 ϵͳ���Ŀɺ��еĺ����빤�ߵ�
			3 һЩ���õĺ��������ݺ�����,�󲿷���C
			4 װ�õ�����˵��,ͨ����/dev�µĵ���
			5 �趨��������ĳЩ�����ĸ�ʽ
			6 ��Ϸ
			7 ������Э����,����linux����ϵͳ,����Э��,ascii code˵����
			8 ϵͳ����Ա���õ�ָ��
			9 ��kernel�йص��ļ�
			NAME ��̵�ָ��,��������˵��
			SYNOPSIS ��̵�ָ���´��﷨���
			DESCRIPTION ��Ϊ������˵��,�ⲿ����ϸ��
			OPTIONS ����﷨������,���оٵ����п��õ�ѡ��˵��
			COMMANDS �������ʽ��ִ��ʱ,�����ڴ˳�ʽ���´��ָ��
			FILES �����ʽ��������ʹ�û�ο������ᵽ��ĳЩ����
			SEE ALSO ���Բο���,�����ָ�����������ص�����˵��
			EXAMPLE һЩ���Բο��ķ���
			BUGS �Ƿ�����ص�bug
		man -f �����ҵ�����
		(�ɲ鿴�������м���˵��)
		man 1-7 �����ҵ�����
		(�򿪶�Ӧ����man�ֲ�)
		man -k man
		(����˵������,ֻҪ��man����ؼ��־ͽ���˵���г���)
	shutdown
		/sbin/shutdown -t �� -arkhncfF ʱ�� ����ѶϢ
			-t �� �������ػ�
			-k ������Ĺػ�,ֻ�Ƿ��;���ѶϢ��ȥ
			-c ȡ���Ѿ��ڽ��е�shutdownָ������
			ʱ�� ����һ��Ҫ����Ĳ���ָ��ϵͳ�ػ���ʱ��
		��:
		/sbin/shutdown -h 10 'i will shutdown after 10mins'
		(���ߴ��,��������ʮ���Ӻ�ػ�)
		shutdown -h now
		(�����ػ�)
		shutdown -h 20:25
		(20:25�ػ�,�糬ʱ������������20:25�ػ�)
		shutdown -h +10
		(10�ֺ��Զ��ػ�)
		shutdown -r now
		(��������)
		shutdown -r +30 'the system will reboot'
		(30�ֺ�����)
		shutdown -k now 'the system will reboot'
		(ֻ����������Ϣ)

***����linux����Ȩ��/Ŀ¼����
	chgrp
		chgrp -R Ŀ¼�����ļ���
			-R �ݹ����
	chown
		chown -R �˺����� ������Ŀ¼
		chown -R �˺�����:������ ������Ŀ¼
			-R �ݹ����
	chmod
		chmod -R xyz ������Ŀ¼
			-R �ݹ����
	uname
		uname -r
	lsb_release
		lsb_release -a

***�ߡ�linux������Ŀ¼����
	Ŀ¼����ز���
		.	����˲�Ŀ¼
		..	������һ��Ŀ¼
		-	����ǰһ������Ŀ¼
		~	����Ŀǰʹ����������ڵļ�Ŀ¼
		~�˺�	�����˺Ŷ�Ӧ������û��ļ�Ŀ¼
	pwd
		pwd -P
			-P ��ʾ��ʵ·��,���������ᵵ·��
	mkdir
		mkdir -mp Ŀ¼����
			-m ֱ���趨Ȩ��,����Ҫ��Ԥ��umask��ɫ
			-p �ݹ齨��
	rmdir
	(ɾ����Ŀ¼)
		rmdir -p Ŀ¼����
			-p �ݹ�ɾ��
	$PATH
		echo $PATH
		PATH=$PATH:·��
	cp
		cp -adfilprsu ��Դ�� Ŀ�굵
		cp options source1 source2 ... directory
			-a ����-pdr
			-p ��ͬ��������һ����,��������Ԥ��ֵ
			-d ����ԴΪ���ᵵ�����������ӵ����Զ��ǵ�������
			-r �ݹ鸴��,����Ŀ¼
			-l ����Ӳ����
			-s ����������
		cp -s bashrc bashrc_slink(������)
		cp -l bashrc bashrc_hlink(Ӳ����)
		cp -d bashrc_slink bashrc_slink_2
	rm
		rm -fir ������Ŀ¼
			-f force
			-i ����ģʽ,ɾ��ǰ����ʾ
			-r �ݹ�ɾ��,������Ŀ¼
	mv
		mv -fiu source destination
		mv options source1 source2 ... directory
	rename
	(����)
	basename
	dirname
	(ȡ�õ������ƻ�Ŀ¼����)
	touch
		touch -acdmt ����
			-a ������access time
			-c �����ĵ�����ʱ��,�������������򲻽����µ���
			-d ����������ĵ�ʱ�������Ŀǰ��ʱ��,Ҳ����ʹ��--date="���ڻ�ʱ��"
			-m ���޸�mtime
			-t ����������ĵ�ʱ�������Ŀǰ��ʱ��,��ʽΪYYMMDDhhmm
	which
	(Ѱ��ִ�е�)
		which -a command
	whereis
	(Ѱ���ض�����,ִ�е���һ�㵵����Ŀ¼)
		whereis -bmsu ������Ŀ¼��
			-b ֻ��binary��ʽ�ĵ���
			-m ֻ����˵����manual·���µĵ���
			-s ֻ��source��Դ����
			-u ������������������Ŀ���е��������⵵��
	locate
		locate -ir keyword
			-i ���Դ�Сд�Ĳ���
			-r ����ɰ������ʾ������ʾ����
	locate��whereis���Ǽ��������ݿ�
	updatedb(�������ݿ�)
	find
		find path option action
			

***�ˡ�linux�ŵ��뵵��ϵͳ
***�š������뵵��ϵͳ�Ĵ��
	gzip,zcat
	(gzip:���Խ⿪compress,zip,gzip��,ѹ����ѹ��������Դ�ļ�)
	(zcat:����ֱ�Ӷ�ȡѹ����������ı�����)
		gzip -cdtv# ����
		zcat ����.gz
			-c ��ѹ���������������Ļ��,��͸���������ص���������
			-d ��ѹ���Ĳ���;
			-t ������������һ��ѹ������һ����,�����������޴���
			-v ������ʾ��ԭ����/ѹ��������ѹ���ȵ���Ϣ
			-# ѹ���ȼ�
		*�ѵ��������ѹ����ѹ��,������ԭ���ĵ���
		 gzip -9 -c man.config > man.config.gz
	bzip2,bzcat
		bzip2 -cdkzv# ����
		bzcat ����.bz2
			-c ��ѹ���Ĺ��̲��������������өĻ��
			-d ��ѹ���Ĳ���
			-k ����ԭʼ����,������ɾ��ԭʼ�ĵ���
			-z ѹ���Ĳ���
			-v ������ʾ��ԭ����/ѹ��������ѹ���ȵ���Ϣ
			-# ��gzipͬ����,ѹ���Ȳ���
	tar(���)
		tar -j|-z cv -f �����ĵ��� filename...
		tar -j|-z tv -f �����ĵ���
		tar -j|-z xv -f �����ĵ��� -C Ŀ¼
			-c ��������ĵ���
			-t �쿴����ĵ�������������Щ����
			-x ���
			-j bzip2
			-z gzip
			-v �ڹ����н����ڴ���ĵ�����ʾ����
			-f ��Ҫ������ĵ���
			-C ���ض�Ŀ¼������
			-p ��������ԭ����Ȩ��������
			-P ��������·��,�������и�Ŀ¼
			--exclude=file ��ѹ�������в�Ҫ��file���
		tar -jxv -f �����.tar.bz2 ���д��⿪�ĵ���
		(��ȫ�����,ֻ�⿪���е��ض��ļ�)
		tar -jcv -f /root/system.tar.bz2 \
		--exclude=/root/etc* \
		--exclude=/root/system.tar.bz2 \
		/etc /root
		(�������ĳЩ����)
		tar -jcv -f /root/abc.tar.bz2 \
		--newer-mtime="2008/09/29" /etc/*
		(�����ĳ�������µĵ���)
		tar -cvf - /etc | tar -xvf -
		(���ù���������������)
		(�뽫/etc�Ķ������Ƶ�һ��Ŀ¼,�����ֲ�����cp -r,���ô���ķ�ʽ������,-��ʾ����ĵ���,�����ֲ������м䵵������)
	dump
	*�������ݵ�����Ϊ��һ����ϵͳ:�Ϳ���ʹ������dump����
	*�����ݵ�����ֻ��Ŀ¼,���ǵ�һ����ϵͳ:dump����������
	 ���еı������϶�����Ҫ�ڸ�Ŀ¼��
	 �ҽ���ʹ��level 0,�༴��֧Ԯ��������
	 ��֧Ԯ-uѡ��,�༴�޷�����/etc/dumpdates���ʱ���¼��
		dump -Suvj -level -f ���ݵ� �����ݵ�����
		dump -W
			-S ���г�����Ĵ�����������Ҫ���ٴ��̿ռ���ܹ�������
			-u �����dump��ʱ���¼��/etc/dumpdates
			-v ��dump�ĵ���������ʾ����
			-j ����bzip2֧��
			-level �ȼ� 0,,,9 ʮ���ȼ�
			-f �е�����tar,����Ӳ����ĵ���,Ҳ���Խ��� /dev/st0װ�õ���
			-W �г���/etc/fstab�������dump�趨�ķ����Ƿ��б��ݹ�
		��:
		dump -S /dev/hdc1
		dump -0u -f /root/boot.dump /boot
	restore
		restore -t -f dumpfile -h
		restore -C -f dumpfile -D
		restore -i -f dumpfile
		restore -r -f dumpfile
			-t ��ģʽ���ڲ쿴dump�ĵ���ʲô����
			-C ���Խ�dump�ڵ����ϸ�ʵ�ʵ����Ƚ�
			-i ���뻥��ģʽ,���Բ��ֻ�ԭ,����Ŀ¼
			-r �������ļ�ϵͳ��ԭ��ģʽ,���ڻ�ԭ����ϵͳ�Ļ�ԭ
			-h �쿴�������������е�inode�뵵��ϵͳlabel����Ϣ
			-f ��Ҫ�����dump����
			-D ��-C���д���,���Բ������ӵĹ��ص���dupm���в�ͬ�ĵ���
		��:
		restore -t -f /root/boot.dump
		restore -C -f /root/boot.dump
		restore -r -f /root/boot.dump(����Ҫ���µ���ϵͳ���ص�����ȥ����)
		restore -i -f /root/etc.dump(���뻥��ģʽ)
		add fil ���ļ���Ŀ¼�������ѹ�ĵ����б�
		delete file ���ļ���Ŀ¼�Ӵ���ѹ�ĵ����б����Ƴ�
		extract ������ѹ�б��е��ļ���Ŀ¼��ѹ����
	mkisofs:����ӳ��
		mkisofs -o ӳ�� -rv -m file �����ݵ��� -V vol\
		-graft-point isodir=systemdir ...
			-o ������Ҫ�������Ǹ�ӳ�񵵵���
			-r ͸��rock ridge����֧Ԯunixlinux�ĵ�������,�ɼ�¼�϶����Ѷ
			-v ��ʾ����iso�����Ĺ���
			-m �ų���������˼ͬexclude
			-V ����Volume,�е���win�п���cd title��
			-graft-point graft��ת�޻���ֲ����˼
		��:
		mkisofs

***ʮ��vim�༭��
	dos2unix
		dos2unix -kn file newfile
			-k �����õ���ԭ����mtimeʱ���ʽ
			-n �����ɵ�,��ת�������������µ�
	unix2dos
		unix2dos -kn file newfile
	(dos2unix,unix2dos:ת��dos��windows�����ַ�)
	iconv
	(ת�����뼯)
		iconv --list
		iconv -f ԭ���� -t �±��� filename -o newfile

ʮһ����ʶ��ѧϰBASH
ʮ���������ʾ��
ʮ����ѧϰshell scripts
***ʮ�ġ�linux�˺Ź�����ACL
	��ʼ��Ⱥ
		passwd�����GID���ǳ�ʼ��Ⱥ,�û�������ʼ��,����Ҫ��group�и������һ����Ӹ��û����û���
	��Ч��Ⱥ
		��Ч��Ⱥ�����������½������󵵰��ĳ�ʼ������
	groups
		�鿴��Ч��Ⱥ
	newgrp
	(�����Ч��)
		newgrp ����
		(����ǰ�û��л�����һ�����״̬,����ԭ��״̬�����ɲ��л�����һ�����shell����,exit���˻ص�ԭ��״̬)
	useradd
	(ֻʹ��useradd�������˺�,�˺Ŵ�����ʱ����״̬,��Ϊshadow����������!!)
		useradd -u UID -g ��ʼ��Ⱥ -G ��Ҫ��Ⱥ -mM -c ˵���� -d ��Ŀ¼����·�� -s shell ʹ�����˺���
			-m ǿ��,Ҫ����ʹ���߼�Ŀ¼(һ���˺�Ԥ��ֵ)
			-M ǿ��,��Ҫ����ʹ���߼�Ŀ¼(ϵͳ�˺�Ԥ��ֵ)
			-r ����һ��ϵͳ�˺�
			-d ָ��ĳ��Ŀ¼��Ϊ��Ŀ¼,����·��
			-s û��ָ������Ԥ��/bin/bash
			-e �˺�ʧЧ����,yyyy-mm-dd
			-f �����Ƿ��ʧЧ,0����ʧЧ
			-l Ϊ��Զ��ʧЧ
	useradd�ο���(����useradd��Ԥ��ֵ)
		useradd -D
	UID,GID,�������Ԥ��ֵ
		/etc/login.defs
	passwd
		passwd --stdin(�����û���,�����˶������������Լ�������)
		passwd -l -u --stdin -S -n ���� -x ���� -w ���� -i ����
�˺�(root����ʹ��)
		��:echo "abc543cc" | passwd --stdin vbird2
			--stdin �����ùܵ���
			-l ��lock����˼,�Ὣshadow�ڶ�������!ʹ����ʧЧ
			-u unlock
			-S �г�������ز���,����shadow�ڴ󲿷���Ϣ
			-n ��ò����޸�����
			-x ��ñ����޸�����
			-w �������ǰ�ľ�������
			-i ����ʧЧ����
	chage
	(����ϸ�����������ʾ����)
		chage -ldEImMW �˺���
			-l �г����˺���ϸ���������
			-d ����,���һ�θ������������,YYYY-MM-DD
			-E ����,�˺�ʧЧ��,YYYY-MM-DD
			-I ����,����ʧЧ����
			-m ����,������̱�������
			-M ����,��������Ҫ���
			-W ����,�������ǰ��������
		��:
		useradd test
		echo "test" | passwd --stdin test
		chage -d 0 test
		(ʹ�����ڵ�һ�ε���ʱ,ǿ������һ��Ҫ�����������ܹ�ʹ��ϵͳ)
	usermod
	(���˺ŵ������Ϣpasswd,shadow���е���)
		usermod -cdefgGalsuLU username(�û��˺�)
			-c ������˺ŵ�˵��,passwd
			-d ������˺ŵļ�Ŀ¼,passwd
			-e ������,YYYY-MM-DD,shadow,�˺�ʧЧ����
			-f ������,shadow,����ʧЧ����
			-g �ӳ�ʼ��Ⱥ,passwd,GID
			-G �Ӵ�Ҫ��Ⱥ,group,�޸�ʹ�����ܹ�
֧Ԯ����Ⱥ(��������)
			-a ��-G����,�����Ӵ�ҪȺ���֧Ԯ
			-l �޸��˺�����,passwd
			-s �����ʵ�ʵ�shell����,/bin/bash��
			-u �����UID������
			-L ��ʱ��ʹ���ߵ����붳��,shadow
			-U �������,shadow
	userdel
	(ɾ��ʹ�����������)
	(ʹ�������������:
	passwd,shadow,group,gshadow
	/home/username,/var/spool/mail/username)
		userdel -r username
			-r ��ͬʹ���߼�Ŀ¼Ҳһ��ɾ��
	finger
	(���ĺܶ�ʹ������ص���Ѷ,�󲿷ֶ�����passwd��)
		finger -s username
			-s ���г�ʹ�����˺�ȫ���ն˴��������ʱ��ȵ�
			-m �г������ӵ��˺���ͬ��,������	���ò��ֱȶ�(����ȫ������)
		��:finger
		   (�ҳ�Ŀǰ��ϵͳ��������ʹ���ߵ���ʱ��,����һЩoffice officephone�ȸ��������Ϣ)
	chfn
	(ʵ����passwd)
	(���ĵ�finger������ʾ���ĵ绰����ظ�����Ϣ)
		chfn -foph �˺�
			-f ����������
			-o �칫�ҵķ������
			-p �繫�ҵĵ绰����
			-h ����ĵ绰����
	chsh
	(�ı�shell)
		chsh -ls
			-l �г�Ŀǰϵͳ������õ�shell
			-s �趨�޸��Լ���shell
		��:chsh -l
		   chsh -s /bin/csh
	id
	(��ѯ�Լ�����ĳ���û������id��Ϣ)
	(�����������ж�ϵͳ�����ǲ��Ǵ���ĳ���û�)
	groupadd
		groupadd -g gid -r Ⱥ������
			-g ����ض���GID,����ֱ�Ӹ���GID
			-r ����ϵͳȺ��
	groupmod
		groupmod -g gid -n group_name Ⱥ����
			-g �޸�GID����
			-n �޸�Ⱥ����
	groupdel
		groupdel Ⱥ������
	gpasswd
		root������:
		gpasswd Ⱥ����
			(�����κβ���,��ʾ������һ������)
		gpasswd -A �û� -M �û� ��Ⱥ
			-A ��������Ȩ���������ʹ���߹���(��Ⱥ��Ĺ���Ա)
			-M ��ĳЩ�˺ż��뵽���Ⱥ����
		gpasswd -rR ��Ⱥ
			-r ���������Ƴ�
			-R ����������ʧЧ
		�����Ա������:
		gpasswd -ad user groupname
			-a ��ʹ���߼��뵽����
			-d ��ʹ�����Ƴ�����
	ACL
		����ACL:
		�ļ�ϵͳ����Ҫ����(dumpe2fs -h /dev/..)
				  (Default mount options)
		mount -o remount,acl /
		vi /etc/fstab
	setfacl
		setfacl -bkRd -m|-x acl���� Ŀ�굵��
			-m �趨������acl����������ʹ��
			-x ɾ��������acl����
			(-m -x �����Ժ���)
			-b �Ƴ����е�acl�趨����
			-k �Ƴ�Ԥ���acl����
			-R �ݹ��趨acl
			-d �趨Ԥ��acl����,ֻ��Ŀ¼��Ч,��Ŀ¼���½������ϻ����ô�Ԥ��ֵ
		��:
		setfacl -m u:vbird1:rx acl-test1
		setfacl -m u::rwx acl-test1
		(�趨�淶:   u:ʹ�����˺��б�:Ȩ��)
		(��ʹ�����б�,�����趨�õ���ӵ����)
		setfacl -m g:mygroup1:rx act-test1
		setfacl -m m:r acl-test1
		(�趨Ԥ����ЧȨ��)
		setfacl -m d:u:myuser1:rx /srv/projuecta
		(��Ŀ¼��������в�����ӵ�д��趨)
		
	getfacl
		getfacl filename
			ѡ�����setfacl��ͬ
	su
	(����л�ָ��)
	(���뱻�л�������)
	(su�����-,�и�û�����кܴ����,��Ϊ�漰��login-shell��non-login shell�ı�����ȡ��ʽ)
		su -lm -c ָ�� username
			- ����ʹ�� - �� su - ����ʹ��login-shell�ı���������ȡ��ʽ������ϵͳ;��ʹ��������û�м���ȥ,������л�Ϊroot�����
			-l �� - ����,��������Ҫ�����л���ʹ�����˺�,Ҳ��login-shell��ʽ
			-m -m��-p��һ����,��ʾʹ��Ŀǰ�Ļ����趨,������ȡ��ʹ���ߵ��趨��
			-c ������һ��ָ��,����-c������Լ���ָ��
		��:
		su(non-login shell��ʽ���root,��������ԭ����)
		su -(login-shell��ʽ���root,�������root����)
		su - -c "head -n 3 /etc/shadow"(��ִ������)
		su -l �û���
	sudo
	(�����л����Լ�������)
		sudo -b -u ��ʹ�����˺�
			-b ��������ָ��ŵ���������ϵͳ����ִ��,������Ŀǰ��shell����Ӱ��
			-u ������Խ����л���ʹ����,���޴���������л����Ϊroot
		��:
		sudo -u sshd touch /tmp/mysshd
		sudo -u vbird1 sh -c "mkdir ~vbird1/www;cd ~vbird1/www;echo 'This is index.html file' > index.html"
	visudo,sudoers
	(vi�޷��༭sudoers)
		root	ALL=(ALL)	ALL
		ʹ����
			�����ߵ���Դ��������
			     ���л������
					���´��ָ��
		%wheel	ALL=(ALL)	ALL
		(����߼���һ��%,��ʾ����ӵ���һ����Ⱥ)
		%wheel 	ALL=(ALL)	NOPASSWD:ALL
		(NOPASSWD������Ҫ�����������ʹ��sudo)
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
	(��ѯʹ����)

ʮ�塢quota,raid,lvm
***ʮ�������й����ų�
	at(atd)
		at -mldv time
		at -c ��������
			-m ��at��ɺ�ʹû�������Ϣ,Ҳ��email֪ͨʹ���߸ù����Ѿ����
			-l �൱��atq,�г�Ŀǰϵͳ�������и�ʹ���ߵ�at�ų�
			-d �൱��atrm,ȡ���ų�
			-v �Խ����Ե�ʱ���ʽ�г�at�ų��еĹ���
			-c �����г�����ӵĹ�����ʵ��ָ������
	crontab(crond)
		crontab -u username -l,-e,-r
			-u ֻ��root���ܽ����������,������ʹ���߽����Ƴ�crontab�ų�
			-e �༭crontab�Ĺ�������
			-l ���Ĺ�������
			-r �Ƴ����й�������,���Ƴ�һ��Ŀ,-e�༭

***ʮ�ߡ����������selinux
	&(ֱ�ӽ�ָ���������ִ��)
		tar -zpcf /tmp/etc.tar.gz /etc &
	ctrl+z(��Ŀǰ�Ĺ���������������ͣ)
	jobs(�۲�Ŀǰ�ı�������״̬)
		jobs -lrs
			-l �����г�job�����ָ�֮��ͬʱ�г�PID�ĺ���
			-r ���г����ڱ���run�Ĺ���
			-s ���г����ڱ�����stop�Ĺ���
	fg(�����������õ�ǰ��������)
		fg %jobnumber
		fg������ȡԤ��ȡ����+�ŵ��Ǹ�����
	bg(�ù����ڱ����µ�״̬���������)
	kill
		kill -signal %jobnumber
		kill -l
			-l �г�Ŀǰkill�ܹ�ʹ�õ�Ѷ������Щ
			-1 ���¶�ȡһ�β������趨������reload
			-2 �������ɼ�������ctrl-cͬ���Ķ���
			-9 ����ǿ��ɾ��һ������
			-15 �������ĳ���ʽ��ֹһ������
			-SINGTERM = -15
	nohup
	(��ϵͳ����������,���߲�����ֹ)
		nohup ָ������� ���ն˻�ǰ���й���
		nohup ָ������� & ���ն˻������й���
	ps
	(����ֱ�ӱ�������ͬ��ѡ��)
	(ps -lֻ�ܲ����Լ�bash����)
	(ps aux��������ϵͳ�����ĳ���)
		ps aux
		ps -lA
		ps axjf
	top
	(��������������״̬)
		top -d ���� |top -bnp
	pstree

***ʮ�ˡ���ʶϵͳ����
ʮ�š���ʶ�������¼��
***��ʮ���������̡�ģ�������loader
	����
		1.BIOS
		2.MBR
		3.�ں�,�ں˼�������
			/boot/vmlinuz
			/boot/initrd
			/lib/modules(�ں�ģ��)
		4.init(inittab)
			/etc/init/rcS.conf->/etc/rc.d/rc.sysinit
			/etc/init/rc.conf
			...
			/etc/rc.d/rc.local
	inittab
		�趨��Ŀ:run level:init�Ķ�����Ϊ:ָ����Ŀ
			1 �趨��Ŀ
			  ����ĸ���Ԫ,����init����Ҫ������Ŀ,ֻ��һ���򵥵Ĵ���˵��
			2 run level
			  ����Ŀ����Щrun level�½���(35����3��5�¶�ִ��)
			3 init�Ķ�����Ŀ
				initdefault	����Ԥ���run level�趨ֵ
				sysinit		����ϵͳ��ʼ���Ķ�����Ŀ
				ctrlaltdel	����ctrl+alt+del���������Ƿ�������¿���
				wait		���������λ�趨��ָ����Ŀ����Ҫִ����ϲ��ܽ������������Ķ���
				respawn		���������λ��ָ����������Ƶ���������������
			4 ָ����Ŀ
			  Ӧ�ÿ��Խ��е�ָ��,ͨ����һЩscript
	�Զ���ģ��
		/etc/sysconfig/modules
		/etc/modprobe.conf
	���������ģ��
		����
			/boot/vmlinuz��/boot/vmlinuz-version
		���Ľ�ѹ������RAM Disk
			/boot/initrd��/boot/initrd-version
		����ģ��
			/lib/modules/version/kernel��/lib/modules/$(uname -r)/kernel
		����ԭʼ��
			/usr/src/linux��/usr/src/kernels(Ҫ��װ����,Ԥ�費��װ)
		���İ汾
			/proc/version
		ϵͳ���Ĺ���
			/proc/sys/kernel
	����ģ����������
		/lib/modules/$(uname -r)/modules.dep
		(��¼�˺���ģ���������)
		depmod -Ane
		(����modules.dep����ļ�)
			�����κβ���,���ؽ�modules.dep����
			-A ֻ�з��ֱ�modules.dep���µ�ģ��ʱ�Ÿ���
			-n ��д��,ֻ�ǽ�����������ʾ����
			-e ��ʾ��Ŀǰ������Ĳ���ִ�е�ģ������
	����ģ�����ʾ
		lsmod
		(��ʾ�Ѿ�������ĵ�ģ��)
		modinfo
		(�����ں����ڵ�ģ��,�����Լ��ĳ��ģ�鵵��)
			modinfo -adln ģ�������ļ���
				-a ���г���������
				-d ���г���ģ���˵��
				-l ���г���ģ�����Ȩ
				-n ���г���ģ�����ϸ·��
	����ģ����������Ƴ�
		insmod
		(�ֶ�����ģ��)
			insmod ����·���������� ����
		rmmod
		(�ֶ��Ƴ�ģ��)
			rmmod -fw ����
				-f ǿ���Ƴ������Ƿ�ʹ��
				-w ������ʹ��,��ʹ��������Ƴ�
		modprobe
			modprobe -lcfr ����
				-c �г�Ŀǰϵͳ���е�ģ��
				-l �г�Ŀǰ��/lib/modules/$(uname -r)/kernel�е�����ģ����������
				-f ǿ�������ģ��
				-r �Ƴ�ģ��

��ʮһ��ϵͳ�趨����
��ʮ����ԭʼ����tarball
��ʮ�������尲װrpm��YUM
��ʮ�ġ�X Window�趨
��ʮ�塢linux���ݲ���
��ʮ����linux���ı��������