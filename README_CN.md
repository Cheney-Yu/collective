# 工具收集笔记

**记录我在VPS研究过程中所使用到的一些工具**

目标是集成一个install.sh程序，通过选择数字规避输入代码部分（懒）


## 目录

### 已完成

+ [代理](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#代理)
    + [Shadowsocks](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#Shadowsocks)
	+ [V2Ray](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#V2Ray)
	+ [Trojan](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#Trojan)
	+ [Trojan-Go](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#Trojan-Go)
	+ [Wireguard](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#Wireguard)
	+ [Socks5 with tls(telegram)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)

+ [中转(NAT)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)
    + [gost](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)
	+ [ufw](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)
	+ [HaProxy](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)

+ [加速](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)
    + [bbr](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)

+ [系统安全](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)
    + [change SSH port](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)
	+ [fail2ban](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)

+ [OpenVZ NAT](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)
    + [bbr plus(OpenVZ)](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)
	+ [V2Ray](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#)

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
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### V2Ray
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### Trojan
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

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



### 中转（NAT机）
> Including gost , ufw , HaProxy

*此部分介绍安装方式*

#### gost
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
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
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**

#### V2Ray
Shadowsocks 采用的是秋水逸冰（@teddysun）的[脚本](https://github.com/teddysun/shadowsocks_install/tree/master)
**内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本**
**内存较小的VPS建议使用Shadowsocks-libev脚本**
**有多端口需求建议使用Shadowsocks-python**
