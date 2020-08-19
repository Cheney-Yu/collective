# 工具收集笔记

**记录我在VPS研究过程中所使用到的一些工具**

目标是集成一个install.sh程序，通过选择数字规避输入代码部分（懒）    
现阶段先将使用到的工具先记录下来，方便使用

## 目录

### 已完成

+ [系统安全](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#系统安全)
    + [change SSH port](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#修改ssh-port)
	+ [fail2ban](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#fail2ban)
	
+ [代理](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#代理)
    + [Shadowsocks](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#Shadowsocks)
	+ [V2Ray](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#V2Ray)
	+ [Trojan](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#Trojan)
	+ [Trojan-Go](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#Trojan-Go)
	+ [Wireguard](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#Wireguard)
	+ [Socks5 with tls(telegram)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#socks5-with-tlstelegram-代理)

+ [中转(NAT)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#中转nat机)
    + [gost](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#gost)
	+ [ufw](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#ufw)
	+ [HaProxy](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#haproxy)

+ [加速](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#VPS加速)
    + [bbr](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#bbr-original)

+ [OpenVZ NAT](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#openvz-nat)
    + [bbr plus(OpenVZ)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#bbr-plusopenvz)
	+ [V2Ray](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#v2ray-1)

### 计划中

+ Speedtest

+ 中转
    + iptables
	+ nftables

+ 探针

+ DD 系统


## 直接键入型使用


### **系统安全**

> Including 修改SSH Port，fail2ban
	
	
- #### **修改SSH Port**
	修改`/etc/ssh/sshd_config`，将
	```bash
	#Port 22
	```
	前面的`#`去掉，将22改成想要的端口，或者在下面加多一行
	```bash
	Port 端口
	```
	
	
- #### **fail2ban** 
	在Debian和Ubuntu系统中 输入`apt-get install fail2ban`即可安装fail2ban       
	如果提示`Package not found`,输入`apt update`先更新系统再安装   
	其它系统（CentOS）的fail2ban安装和fail2ban管理，请参照[fail2ban](https://github.com/fail2ban/fail2ban)
	
	
	
----
### **代理**

> Including Shadowsocks , V2Ray , Trojan , Trojan-Go, WireGuard

    
- #### **Shadowsocks**
	Shadowsocks 采用的是秋水逸冰（@teddysun）的[Shadowsocks安装脚本](https://github.com/teddysun/shadowsocks_install/tree/master)

	##### 内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本
	```bash
	wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
	chmod +x shadowsocks-all.sh
	./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
	```

	##### 内存较小的VPS建议使用Shadowsocks-libev脚本

	Debian系统
	```bash
	    wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev-debian.sh
	    chmod +x shadowsocks-libev-debian.sh
	    ./shadowsocks-libev-debian.sh 2>&1 | tee shadowsocks-libev-debian.log
	```
	其它系统
	```bash
	    wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev.sh
	    chmod +x shadowsocks-libev.sh
	    ./shadowsocks-libev.sh 2>&1 | tee shadowsocks-libev.log
	```

	##### 有多端口需求建议使用Shadowsocks-python
	
	
	
- #### **V2Ray**
	
	
	```
	```
	
	
	
- #### **Trojan**
	Trojan 采用的是Jrohy（@Jrohy）的[带有Web管理界面的脚本](https://github.com/Jrohy/trojan)    
	需提前将IP地址解析到域名

	##### 一键脚本安装
	```bash
	#安装/更新
	source <(curl -sL https://git.io/trojan-install)

	#卸载
	source <(curl -sL https://git.io/trojan-install) --remove

	```
	安装完后输入'trojan'可进入管理程序   
	浏览器访问 https://域名 可在线web页面管理trojan用户  
	前端页面源码地址: [trojan-web](https://github.com/Jrohy/trojan-web)
	
	
- #### **Trojan-GO**
	
	```
	```
		
- #### **WireGuard**
	
	```
	```
	
	
- #### **Socks5 with Tls(Telegram 代理)**
	考虑到很多商家禁止MTProto的搭建和使用，我们的Telegram代理多采用Socks5代理     
	考虑到安全性，建议的方式是使用[gost](https://github.com/ginuerzh/gost)搭建带有tls的Socks5代理 

	##### gost的安装
	先安装wget
	```bash
	# Debian和Ubuntu系统下安装wget
	apt-get update -y && apt-get install wget -y
	# CentOS系统下安装wget
	yum update -y && yum install wget -y
	```
	再安装gost
	```bash
	wget -N --no-check-certificate https://github.com/ginuerzh/gost/releases/download/v2.11.1/gost-linux-amd64-2.11.1.gz && gzip -d gost-linux-amd64-2.11.1.gz
	mv gost-linux-amd64-2.11.1 gost
	chmod +x gost
	```

	搭建socks5代理     
	```bash
	./gost -L 用户名:密码@:端口 socks5+tls://:端口
	```
	
 ----
### **中转(NAT机)**

> Including gost , ufw , HaProxy
	
*此部分介绍安装方式*     
	
	
参考文章：     
[利用 NAT VPS 进行流量中转](https://blog.chaos.run/dreams/nat-vps-port-forwarding/)
	
	
- #### **gost**
	[gost脚本地址](https://github.com/ginuerzh/gost) 

	##### gost的安装
	先安装wget
	```bash
	# Debian和Ubuntu系统下安装wget
	apt-get update -y && apt-get install wget -y
	# CentOS系统下安装wget
	yum update -y && yum install wget -y
	```
	再安装gost
	```bash
	wget -N --no-check-certificate https://github.com/ginuerzh/gost/releases/download/v2.11.1/gost-linux-amd64-2.11.1.gz && gzip -d gost-linux-amd64-2.11.1.gz
	mv gost-linux-amd64-2.11.1 gost
	chmod +x gost
	```

- #### **ufw**
	
	ufw的安装       
	Ubuntu系统下默认已安装ufw     
	```bash
	# Debian系统下安装ufw
	apt-get update -y && apt-get install ufw -y
	```
	
	
- #### **HaProxy**
	
	```
	```
	
	
	
 ----

### **VPS加速**

> Including BBR
    
    
- #### **BBR Original**     
	修改`/etc/sysctl.conf`，在下方加入
	```bash
	net.core.default_qdisc = fq
	net.ipv4.tcp_congestion_control = bbr
	```
	使其生效
	```bash
	sysctl -p
	```
	查看BBR是否开启成功
	执行如下命令，如果返回值中有BBR则说明开启成功
	```bash
	sysctl net.ipv4.tcp_congestion_control
	```
	执行如下命令，如果返回值中有tcp_bbr模块则说明开启成功
	```bash
	lsmod | grep bbr
	```





 ----
### **OpenVZ NAT**

> Including BBR Plus, V2Ray

    
- #### **BBR Plus（OpenVZ）**
	OpenVZ下的BBR-Plus采用的是mzz2017（@mzz2017）的[OpenVZ下开启BBR Plus的脚本](https://github.com/mzz2017/lkl-haproxy)
	
	`lkl` mode via `haproxy`, works for `OpenVZ` virtualization.
	
	##### NOTICE :
		`TUN/TAP` is needed. `256M free memory` is needed.

	##### Usage
	
	```bash
	# for centos
	bash <(curl -Ls https://github.com/mzz2017/lkl-haproxy/raw/master/lkl-haproxy-centos-nocheckvirt.sh)
	
	# for debian
	bash <(curl -Ls https://github.com/mzz2017/lkl-haproxy/raw/master/lkl-haproxy-debian-nocheckvirt.sh)
	
	```


    
- #### **V2Ray**
	OpenVZ下的V2Ray采用的是233boy（@233boy）的[V2Ray一键安装脚本](https://github.com/233boy/v2ray/wiki/V2Ray一键安装脚本)     
	使用 root 用户输入下面命令安装或卸载
	```
	bash <(curl -s -L https://git.io/v2ray.sh)
	```
	> 如果提示 curl: command not found ，那是因为你的 VPS 没装 Curl    
	ubuntu/debian 系统安装 Curl 方法: `apt-get update -y && apt-get install curl -y`    
	centos 系统安装 Curl 方法: `yum update -y && yum install curl -y`    
	安装好 curl 之后就能安装脚本了
	
	备注：安装完成后，输入 v2ray 即可管理 V2Ray     
	如果提示你的系统不支持此脚本，那么请尝试更换系统
