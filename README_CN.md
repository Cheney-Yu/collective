# 工具收集笔记

**记录我在VPS研究过程中所使用到的一些工具**

目标是集成一个install.sh程序，通过选择数字规避输入代码部分（懒）


## 目录

### 已完成

+ [代理](https://github.com/Cheney-Yu/collective/blob/master/README_CN.md#代理)
    + Shadowsocks
	+ V2Ray
	+ Trojan
	+ Trojan-Go
	+ Wireguard
	+ Socks5 with tls(telegram)

+ 中转(NAT)
    + gost
	+ ufw
	+ HaProxy

+ 加速
    + bbr

+ 系统安全
    + change SSH port
	+ fail2ban

+ OpenVZ NAT
    + bbr plus(OpenVZ)
	+ V2Ray

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
##### 内存空间较为充裕的VPS建议使用Shadowsocks-4in1脚本
##### 内存较小的VPS建议使用Shadowsocks-libev脚本
##### 有多端口需求建议使用Shadowsocks-python
