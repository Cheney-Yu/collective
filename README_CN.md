# 工具收集笔记

**记录我在VPS研究过程中所使用到的一些工具**

目标是集成一个install.sh程序，通过选择数字规避输入代码部分（懒）    
现阶段先将使用到的工具先记录下来，方便使用    
Special Thanks:    
	teddysun(https://teddysun.com/category/tech)

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
	+ [UFW](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#ufw)
	+ [HaProxy](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#haproxy)

+ [加速](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#VPS加速)
    + [BBR Original(Recommended)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#bbr-original)
    + [BBR-ALL(teddysun)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#bbr-all)
    + [BBR-Plus(chiakge)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#bbr-chiakge) 

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
	Shadowsocks 采用的是teddysun（@teddysun）的[Shadowsocks安装脚本](https://github.com/teddysun/shadowsocks_install/tree/master)

	- ##### 内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本[参考](https://github.com/ishen7/Blog/issues/2)

		```bash
		wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
		chmod +x shadowsocks-all.sh
		./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
		```

	- ##### 内存较小的VPS建议使用Shadowsocks-libev脚本

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

	- ##### 有多端口需求建议使用
		```
		```
		
	Shadowsocks搭建建议[使用AEAD加密](https://zhuanlan.zhihu.com/p/28566058) 如    
		> AES-128-GCM    
		AES-192-GCM    
		AES-256-GCM    
		ChaCha20-IETF-Poly1305    
		XChaCha20-IETF-Poly1305  
		
	> CPU设备建议使用`AES-XXX-GCM`系列    移动设备建议使用`ChaCha20-IETF-Poly1305`系列    
	
	
- #### **V2Ray**    
	需提前将IP地址解析到域名
    
	- #### [Vmess+websocket+TLS+Nginx+Website的wulabing版本](https://github.com/wulabing/V2Ray_ws-tls_bash_onekey)   
		系统支持：Debian 9+ / Ubuntu 18.04+ / Centos7+     
		安装脚本	
		```bash
		wget -N --no-check-certificate -q -O install.sh "https://raw.githubusercontent.com/wulabing/V2Ray_ws-tls_bash_onekey/master/install.sh" && chmod +x install.sh && bash install.sh
		```
		查看客户端配置    
		`cat ~/v2ray_info.txt`  

		启动方式    
		> 启动 V2ray：`systemctl start v2ray`    
		停止 V2ray：`systemctl stop v2ray`    
		启动 Nginx：`systemctl start nginx`    
		停止 Nginx：`systemctl stop nginx`   

		相关目录    
		> Web 目录：`/home/wwwroot/3DCEList`    
		V2ray 服务端配置：`/etc/v2ray/config.json`    
		V2ray 客户端配置: `~/v2ray_info.inf`    
		Nginx 目录：`/etc/nginx`    
		证书文件:`/data/v2ray.key`和`/data/v2ray.crt`请注意证书权限设置
	
	
	
	- #### [带有多用户管理的multi-v2ray版本](https://github.com/Jrohy/multi-v2ray)    
		> 注意：此版本默认采用的是mkcp传输配置    
		
		系统支持：   
		安装脚本	
		```bash
		source <(curl -sL https://multi.netlify.app/v2ray.sh) --zh
		```
		升级命令(保留配置文件更新)
		```bash
		source <(curl -sL https://multi.netlify.app/v2ray.sh) -k
		```
		卸载命令
		```bash
		source <(curl -sL https://multi.netlify.app/v2ray.sh) --remove
		```
		命令行参数
		```bash
		v2ray [-h|--help] [options]
		    -h, --help           查看帮助
		    -v, --version        查看版本号
		    start                启动 V2Ray
		    stop                 停止 V2Ray
		    restart              重启 V2Ray
		    status               查看 V2Ray 运行状态
		    new                  重建新的v2ray json配置文件
		    update               更新 V2Ray 到最新Release版本
		    update.sh            更新 multi-v2ray 到最新版本
		    add                  新增mkcp + 随机一种 (srtp|wechat-video|utp|dtls|wireguard) header伪装的端口(Group)
		    add [wechat|utp|srtp|dtls|wireguard|socks|mtproto|ss]     新增一种协议的组，端口随机,如 v2ray add utp 为新增utp协议
		    del                  删除端口组
		    info                 查看配置
		    port                 修改端口
		    tls                  修改tls
		    tfo                  修改tcpFastOpen
		    stream               修改传输协议
		    cdn                  走cdn
		    stats                v2ray流量统计
		    iptables             iptables流量统计
		    clean                清理日志
		    log                  查看日志
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
	[来自于teddysun的WireGuard一键安装脚本](https://teddysun.com/554.html)    
	系统支持：CentOS 7+，Debian 8+，Raspbian 10，Ubuntu 16+，Fedora 29+    
	内存要求：≥256M    
	使用 root 用户登录系统，运行以下命令下载脚本，赋予执行权限：    
	```bash
	wget --no-check-certificate -O /opt/wireguard.sh https://raw.githubusercontent.com/teddysun/across/master/wireguard.sh
	chmod 755 /opt/wireguard.sh
	```
	    
	    
	从代码编译安装 WireGuard
	```bash
	/opt/wireguard.sh -s
	```
	从 repository 直接安装 WireGuard
	```bash
	/opt/wireguard.sh -r
	```
	    
	安装完成后，脚本提示如下    	
	```bash
	WireGuard VPN Server installation completed    
	WireGuard VPN default client file is below:    
	/etc/wireguard/wg0_client    
	WireGuard VPN default client QR Code is below:    
	/etc/wireguard/wg0_client.png    
	Download and scan this QR Code with your phone    
	Welcome to visit: https://teddysun.com/554.html    
	Enjoy it
	```
	
	查看已安装 WireGuard 版本号    
	`/opt/wireguard.sh -v`    
	编译升级 WireGuard 到当前最新版本    
	`/opt/wireguard.sh -u`    
	新增 WireGuard 客户端配置    
	`/opt/wireguard.sh -a`    
	列出 WireGuard 客户端配置    
	`/opt/wireguard.sh -l`    
	
	
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
	其中，`用户名` `密码`为所搭建的socks5代理的用户名和密码，`端口` 为搭建的socks5代理监听的端口
	
 ----
### **中转(NAT机)**

> Including gost , ufw , HaProxy
	
*此部分介绍安装方式*     
	
	
参考文章：     
[利用 NAT VPS 进行流量中转](https://blog.chaos.run/dreams/nat-vps-port-forwarding/)
	
	
- #### [**gost**](https://docs.ginuerzh.xyz/gost/)
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

- #### **UFW**
	
	此方法在 Debian & Ubuntu 下较为简便（Ubuntu 18.04 默认使用 UFW）。    
	
	```bash
	# Debian系统下安装ufw
	apt-get update -y && apt-get install ufw -y
	```

	首先要修改 `/etc/sysctl.conf` 文件：
	
	```bash
	echo "net.ipv4.ip_forward = 1" | tee -a /etc/sysctl.conf
	sysctl -p
	```
	修改 `/etc/default/ufw` ：
	```bash
	# /etc/default/ufw
	DEFAULT_FORWARD_POLICY="ACCEPT"
	```
	修改 `/etc/ufw/before.rules` ：
	```bash
	# 在 *filter 之前添加：
	# /etc/ufw/before.rules 
	
	# nat table rules
	*nat
	:PREROUTING ACCEPT [0:0]
	:POSTROUTING ACCEPT [0:0]

	# port forwarding
	-A PREROUTING -p tcp --dport 本机端口号 -j DNAT --to-destination 目标地址:目标端口号
	-A PREROUTING -p udp --dport 本机端口号 -j DNAT --to-destination 目标地址:目标端口号
	-A POSTROUTING -p tcp -d 目标地址 --dport 目标端口号 -j SNAT --to-source 本机内网地址
	-A POSTROUTING -p udp -d 目标地址 --dport 目标端口号 -j SNAT --to-source 本机内网地址

	# commit to apply changes
	COMMIT
	```
	其中，`目标地址` 为目标服务器的 IP 地址，`本机内网地址` 为本机在内部局域网的 IP 地址。
	
	重启 UFW：
	`
	ufw disable && ufw enable
	`
	至此，利用 UFW 设置中转的方法介绍完毕。另可根据使用场景，对目标机的防火墙进行配置，令其只接受来自此 NAT VPS 的流量。
	
	
- #### **HaProxy**
	
	```
	```
	
	
	
 ----

### **VPS加速**

> Including BBR , BBR-ALL(teddysun) , BBR-Plus(CentOS) , Linux-NetSpeed(chiakge)
    
    
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

- #### **BBR All**
	来自[teddysun的多系统bbr加速脚本](https://teddysun.com/489.html)    
	系统支持：CentOS 6+，Debian 8+，Ubuntu 16+    
	虚拟技术：OpenVZ 以外的，比如 KVM、Xen、VMware    
	内存要求：≥128M    
	
	使用root用户登录，运行以下命令：
	```bash
	wget --no-check-certificate -O /opt/bbr.sh https://github.com/teddysun/across/raw/master/bbr.sh
	chmod 755 /opt/bbr.sh
	/opt/bbr.sh
	```
	安装完成后，脚本会提示需要重启 VPS，输入 `y` 并回车后重启。
	重启完成后，进入 VPS，验证一下是否成功安装最新内核并开启 TCP BBR，输入以下命令：
	```bash
	uname -r
	```
	查看内核版本，显示为最新版就表示 OK 了    
	输入  
	```bash
	sysctl net.ipv4.tcp_available_congestion_control
	```
	返回值一般为：
	`net.ipv4.tcp_available_congestion_control = bbr cubic reno`     
	或者为：
	`net.ipv4.tcp_available_congestion_control = reno cubic bbr`    
	输入    
	```bash
	sysctl net.ipv4.tcp_congestion_control
	```
	返回值一般为：
	`net.ipv4.tcp_congestion_control = bbr`    
	输入    
	```bash
	sysctl net.core.default_qdisc
	```
	返回值一般为：
	`net.core.default_qdisc = fq`    
	输入
	```bash
	lsmod | grep bbr
	```
	返回值有 `tcp_bbr` 模块即说明 bbr 已启动。注意：并不是所有的 VPS 都会有此返回值，若没有也属正常。    
	
	
	
- #### **BBR (Chiakge)**    

	- ##### [CentOS 系统 ](https://github.com/cx9208/bbrplus) 
		```bash
		wget "https://github.com/cx9208/bbrplus/raw/master/ok_bbrplus_centos.sh" && chmod +x ok_bbrplus_centos.sh && ./ok_bbrplus_centos.sh
		```    
		安装后，执行`uname -r`，显示`4.14.129-bbrplus`则切换内核成功
		执行```lsmod | grep bbr```，显示有`bbrplus`则开启成功    
	
	
	- ##### [Linux-NetSpeed](https://github.com/chiakge/Linux-NetSpeed)
		```bash
		wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh"
		chmod +x tcp.sh
		./tcp.sh
		```
		> 注意：在实际运行中发现运行该脚本时会有CPU占用达到10%-20%的情况 原因不明 请视情况选取合适加速方式
	
	

 ----
### **OpenVZ NAT**

> Including BBR Plus, V2Ray

    
- #### **BBR Plus（OpenVZ）**
	OpenVZ下的BBR-Plus采用的是mzz2017（@mzz2017）的[OpenVZ下开启BBR Plus的脚本](https://github.com/mzz2017/lkl-haproxy)
	
	`lkl` mode via `haproxy`, works for `OpenVZ` virtualization.
	
	NOTICE :`TUN/TAP` is needed. `256M free memory` is needed.

	##### Usage
	
	```bash
	# for centos
	bash <(curl -Ls https://github.com/mzz2017/lkl-haproxy/raw/master/lkl-haproxy-centos-nocheckvirt.sh)
	
	# for debian
	bash <(curl -Ls https://github.com/mzz2017/lkl-haproxy/raw/master/lkl-haproxy-debian-nocheckvirt.sh)	
	```


    
- #### **V2Ray**
	OpenVZ 下的 V2Ray 采用的是 233boy（@233boy） 的 [V2Ray 一键安装脚本](https://github.com/233boy/v2ray/wiki/V2Ray一键安装脚本)     
	使用 root 用户输入下面命令安装或卸载
	```bash
	bash <(curl -s -L https://git.io/v2ray.sh)
	```
	> 如果提示 curl: command not found ，那是因为你的 VPS 没装 Curl    
	ubuntu/debian 系统安装 Curl 方法: `apt-get update -y && apt-get install curl -y`    
	centos 系统安装 Curl 方法: `yum update -y && yum install curl -y`    
	安装好 curl 之后就能安装脚本了
	
	备注：安装完成后，输入 v2ray 即可管理 V2Ray     
	如果提示你的系统不支持此脚本，那么请尝试更换系统
