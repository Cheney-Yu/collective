# 工具收集笔记

**记录我在VPS研究过程中所使用到的一些工具**

目标是集成一个install.sh程序，通过选择数字规避输入代码部分（懒）
现阶段先将使用到的工具先记录下来，方便使用

## 目录

### 已完成

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

+ [系统安全](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#系统安全)
    + [change SSH port](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#修改ssh-port)
	+ [fail2ban](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#fail2ban)

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

### 代理
> Including Shadowsocks , V2Ray , Trojan , Trojan-Go, WireGuard

#### Shadowsocks
Shadowsocks 采用的是秋水逸冰（@teddysun）的[Shadowsocks安装脚本](https://github.com/teddysun/shadowsocks_install/tree/master)

**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**

    wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
    chmod +x shadowsocks-all.sh
    ./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log

**内存较小的VPS建议使用Shadowsocks-libev脚本**

Debian系统

    wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev-debian.sh
    chmod +x shadowsocks-libev-debian.sh
    ./shadowsocks-libev-debian.sh 2>&1 | tee shadowsocks-libev-debian.log

其它系统

    wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev.sh
    chmod +x shadowsocks-libev.sh
    ./shadowsocks-libev.sh 2>&1 | tee shadowsocks-libev.log


**有多端口需求建议使用Shadowsocks-python**


#### V2Ray



#### Trojan
Trojan 采用的是Jrohy（@Jrohy）的[带有Web管理界面的脚本](https://github.com/Jrohy/trojan)
需提前将IP地址解析到域名
#####  a. 一键脚本安装
```
#安装/更新
source <(curl -sL https://git.io/trojan-install)

#卸载
source <(curl -sL https://git.io/trojan-install) --remove

```
安装完后输入'trojan'可进入管理程序   
浏览器访问 https://域名 可在线web页面管理trojan用户  
前端页面源码地址: [trojan-web](https://github.com/Jrohy/trojan-web)

##### b. docker运行
1. 安装mysql  
因为mariadb内存使用比mysql至少减少一半, 所以推荐使用mariadb数据库
```
docker run --name trojan-mariadb --restart=always -p 3306:3306 -v /home/mariadb:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=trojan -e MYSQL_ROOT_HOST=% -e MYSQL_DATABASE=trojan -d mariadb:10.2
```
端口和root密码以及持久化目录都可以改成其他的

2. 安装trojan
```
docker run -it -d --name trojan --net=host --restart=always --privileged jrohy/trojan init
```
运行完后进入容器 `docker exec -it trojan bash`, 然后输入'trojan'即可进行初始化安装   

 启动web服务: `systemctl start trojan-web`   

 设置自启动: `systemctl enable trojan-web`

 更新管理程序: `source <(curl -sL https://git.io/trojan-install)`

#### Trojan-GO
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### WireGuard
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### Socks5 with Tls(Telegram 代理)
Telegram代理采用的是使用[gost](https://github.com/ginuerzh/gost)搭建带有tls的Socks5代理
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

### 中转（NAT机）
> Including gost , ufw , HaProxy

*此部分介绍安装方式*
参考文章：
[利用 NAT VPS 进行流量中转](https://blog.chaos.run/dreams/nat-vps-port-forwarding/)

#### gost
gost[脚本地址](https://github.com/ginuerzh/gost)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### ufw
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### HaProxy
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**


### VPS加速
> Including BBR

#### BBR Original
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

### 系统安全
> Including 修改SSH Port，fail2ban

#### 修改SSH Port
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### fail2ban
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

### OpenVZ Nat
> Including BBR Plus, V2Ray

#### BBR Plus（OpenVZ）
OpenVZ下的BBR-Plus采用的是mzz2017（@mzz2017）的[OpenVZ下开启BBR Plus的脚本](https://github.com/mzz2017/lkl-haproxy)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### V2Ray
OpenVZ下的V2Ray采用的是233boy（@233boy）的[V2Ray一键安装脚本](https://github.com/233boy/v2ray/wiki/V2Ray一键安装脚本)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**
