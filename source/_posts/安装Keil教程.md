---
title: 安装Keil教程
toc: true
tags: 单片机
categories:
  - 嵌入式
  - 软件
abbrlink: 15431
date: 2020-04-06 10:15:36
---

### 背景介绍

keil作为目前最常用的单片机开发IDE，是我们从事嵌入式开发的主要开发工具。在Keil上我们可以用底层的汇编语言或者C语言。本来只能用来开发51单片机后来被ARM公司收购，扩展了它的开发范围，也可用于ARM的开发，使用范围更广了。

本文将简单介绍Keil软件的安装以及对应的STM32的开发所需准备工作。

### 下载安装Keil

到Keil官网：[Keil官网](https://www.keil.com/download/product/)选择所需要安装的版本，我们需要的版本是ARM的，所以下载MDK

-ARM：

![下载MDK.png](https://s1.ax1x.com/2020/04/06/GsKumq.png)

安装包下载好了直接无脑安装，不断Next即可。

从keil5开始，我们需要自己下载所要用的MCU型号的支持芯片包。

直接去网址：[keil5所需pack下载网址](https://www.keil.com/dd2/pack/)

![keil的pack下载安装.png](https://s1.ax1x.com/2020/04/06/GsMHPO.png)

这个部分完成后，我们可以看到keil软件的配置栏：

![Gs1gG8.png](https://s1.ax1x.com/2020/04/06/Gs1gG8.png)

就有我们所要用的芯片的包了，每次使用keil写工程的时候都要进行选择，所以必须保证自己使用的没有问题。

## 参考资料
> - [keil的百度百科](https://baike.baidu.com/item/keil/4082184?fr=aladdin)
