---
title: AWS服务器搭建V2ray教程
tags:
  - VPN
abbrlink: 13864
date: 2020-04-01 17:38:50
categories: 
- Linux
- 服务器
---

笔者于2020年申请了一张VISA信用卡，于是用来申请云服务器，本来想申请google的服务器的，但是因为google取消了VISA的申请，就退而求其次使用了AWS，留此教程。

首先我们需要选取一个服务器的地址，常用的服务器地址有香港、日本、新加坡等等，确定服务器的选取地址可以使用在线ping（[https://www.feitsui.com/zh-hans/cloud/aws](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.feitsui.com%2Fzh-hans%2Fcloud%2Faws)），ping对应的网址观察TTL即可，选取最短TTL的服务器。
新建AWS EC2服务器后启动实例——选择免费的方案并且开始实例，记住一定要使用弹性IP地址并匹配。还要记得V2ray必须要有域名，可以申请或购买。
（参考连接：[https://segmentfault.com/a/1190000019201071](https://links.jianshu.com/go?to=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000019201071)）
XShell链接上服务器之后（服务器连接教程：[https://www.acoro.net/xshell-aws-ec2/](https://links.jianshu.com/go?to=https%3A%2F%2Fwww.acoro.net%2Fxshell-aws-ec2%2F)）
还要注意服务器和虚拟机不太一样，服务器它没有密码，用户名为ubuntu，每次启动su需要写命令sudo su。
进入su之后可以执行V2ray一键安装脚本（参考链接：[https://github.com/ActiveIce/V2Ray_ws-tls_bash_onekey](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FActiveIce%2FV2Ray_ws-tls_bash_onekey)）
执行该命令后选择安装在ws和h2合并之后安装方式固定。
执行脚本确定时间相差不大后选择安装，安装完成后仍在管理员权限下执行./install.sh
打开bbr加速，并加载加速模块FQ。不同的加速模块效果不同。
执行完毕后再进入一次，执行系统配置优化，服务器会在这时重启。
重启后即可正常使用，目前一切正常。