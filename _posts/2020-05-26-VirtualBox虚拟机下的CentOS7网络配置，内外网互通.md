---
layout:     post                    # 使用的布局（不需要改）
title:      VirtualBox虚拟机下的CentOS7网络配置，内外网互通        # 标题 
subtitle:   cenos服务器网络设置	# 副标题
date:       2020-05-26              # 时间
author:     Kay                     # 作者
header-img: img/post-bg-2015.jpg    # 这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               # 标签
    - linux
    - 
---

1. 管理 ——> 全局设定 ——> 网络，新加网络，如图所示（Natnetwork），其他全部默认即可
![新增网卡](https://upload-images.jianshu.io/upload_images/23466769-eb645c29031ac839.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/600)


2. 具体虚拟机设置，网络设置，网卡1选择桥接网络（我这里本机是无线wifi，所以名称是Wireless），高级里面将接入网线打勾，这一步是你的虚拟机能够和主机互通的必要条件
![网卡连接方式-桥接模式](https://upload-images.jianshu.io/upload_images/23466769-575488c3852371a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/600)


3. 继续设置网卡2，这里链接方式选择，Nat网络，然后名称会自动匹配到你第一步全局设置的Nat网络名，高级里面将接入网线打勾，这一步是你的虚拟机能够联通外网的必要条件
![网卡连接方式-Net直连](https://upload-images.jianshu.io/upload_images/23466769-80dbdb80f2311573.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)


4. 运行虚拟机，打开终端，关闭防火墙  否则PING不通宿主机。
	```
	systemctl stop firewalld.service		#停止firewall  
	systemctl disable firewalld.service		#禁止firewall开机启动
	```


5. 接着进入超级管理员模式，用于修改网络配置文件

	```
	su		# 这一步还需要输入管理员密码
	cd /etc/sysconfog/net-scripts		#进入文件所在目录
	vim  ifcfg-enp0s3		#编辑文件
	```
	以下为配置说明和配置案例（图片），了解以下即可

	```
	DEVICE=物理设备名
	IPADDR=IP地址
	NETMASK=掩码值
	NETWORK=网络地址
	BROADCAST=广播地址
	GATEWAY=网关地址
	ONBOOT=[yes|no]（引导时是否激活设备）
	USERCTL=[yes|no]（非root用户是否可以控制该设备）
	BOOTPROTO=[none|static|bootp|dhcp]（引导时不使用协议|静态分配|BOOTP协议|DHCP协议）
	HWADDR = 你的MAC地址
	```
	![](https://upload-images.jianshu.io/upload_images/23466769-716aa1af8ccdff8b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/600)

	![](https://upload-images.jianshu.io/upload_images/23466769-106f2c842c931d66.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/600)

	修改好后保存退出，（需要有管理员权限才能保存，所以前面需要su命令进入管理员模式）


6. 重启虚拟机网络服务  
	`systemctl restart network`


7. 测试
	ping主机ip和www.baidu.com均可以ping通

