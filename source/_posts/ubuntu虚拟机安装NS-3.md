---
title: ubuntu虚拟机安装NS-3
toc: true
tags: 环境
categories:
  - Linux
  - 虚拟机
abbrlink: 30549
date: 2020-04-03 13:48:43
---

## 关于NS-3的介绍：

官网: [http://www.nsnam.org/](https://links.jianshu.com/go?to=http%3A%2F%2Fwww.nsnam.org%2F)
Wiki: [http://www.nsnam.org/wiki/index.php/Main_Page](https://links.jianshu.com/go?to=http%3A%2F%2Fwww.nsnam.org%2Fwiki%2Findex.php%2FMain_Page)
NS-3的包下载地址：
[http://code.nsnam.org/ns-3-dev](http://code.nsnam.org/ns-3-dev](https://links.jianshu.com/go?to=http%3A%2F%2Fcode.nsnam.org%2Fns-3-dev%5D(http%3A%2F%2Fcode.nsnam.org%2Fns-3-dev)
可以安装mercurial之后访问官网下载，下载最新版本解压后放进虚拟机也可以。

## 安装NS-3的步骤：

已经确定安装环境为Ubuntu虚拟机了，暂时不考虑其他结果，之后可以用wsl试一试是否能正常安装，后续在补充相关内容。

### NS-3预安装（安装各种依赖）

首先得修改一下源：
将`/etc/apt/source.list`中的内容删除，更改成清华源或者阿里源。
阿里源：
\#默认注释了源码镜像以提高 apt update 速度，如有需要可自行注释

\#默认注释了源码镜像以提高 apt update 速度，如有需要可自行注释
   >deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
   >deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
   >deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
   >deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
   >deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
   >deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
   >deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
   >deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse

>\#预发布软件源，不建议启用
>deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-proposed main restricted universe multiverse
>deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-proposed main restricted universe multiverse

清华源和中科大源在校园网情况下会快一点，但是未必快很多。
#### 预安装准备：

首先更新源：sudo apt update,sudo apt uograde;

安装一系列依赖：
`>sudo apt-get install gcc g++ python python-dev  
>sudo apt-get install mercurial  
>sudo apt-get install bzr  
>sudo apt-get install gdb valgrind  
>sudo apt-get install gsl-bin libgsl0-dev libgsl0ldbl    //这句在执行时出现错误，后边会解释
>sudo apt-get install flex bison libfl-dev  
>sudo apt-get install tcpdump  
>sudo apt-get install sqlite sqlite3 libsqlite3-dev  
>sudo apt-get install libxml2 libxml2-dev  
>sudo apt-get install libgtk2.0-0 libgtk2.0-dev  
>sudo apt-get install vtun lxc  
>sudo apt-get install uncrustify  
>sudo apt-get install doxygen graphviz imagemagick  
>sudo apt-get install python-sphinx dia        
>sudo apt-get install python-pygraphviz python-kiwi python-pygoocanvas libgoocanvas-dev  
>sudo apt-get install qt4-qmake   
>sudo apt-get install qt4-dev-tools //这个是后边NetAnim仿真界面需要依赖的软件包
>sudo apt-get install libboost-signals-dev libboost-filesystem-dev
>sudo apt-get install openmpi-bin openmpi-doc libopenmpi-dev`

关于错误的解释：

![GUiFfJ.png](https://s1.ax1x.com/2020/04/03/GUiFfJ.png)

按照中文的解释进行相应的替换即可，可以解决问题。
#### 关于NS-3安装包
可以直接从官网下载：[NS-3下载官网](https://www.nsnam.org/releases/)，下载最新版本：

![GUiuTO.png](https://s1.ax1x.com/2020/04/03/GUiuTO.png)

下载后通过VM-tools放进虚拟机中解压即可，最为简单粗暴。
另一种方式是通过wget命令从网上拉下来：
`wget http://www.nsnam.org/release/ns-allinone-3.30.tar.bz2`
或者通过mercurial下载：
`hg clone [http://code.nsnam.org/ns-3-dev](http://code.nsnam.org/ns-3-dev)`
解压的命令：`tar -xjvf ns-allinone-3.30.tar.bz2`

#### 配置NS-3
若你是第一次使用NS-3，则解压后进入对应目录，执行以下命令
`sudo ./build.py`
这条命令是第一次安装必备的，之后就可以直接用waf编译执行。
`sudo ./waf -d optimized -enable-examples -enable-tests configure`
以上为配置configuration，配置完毕后之后都要用./waf执行。
这个命令会检查之前安装的依赖，如果缺少会报错或者中断，要注意一定把所有需要的依赖安装完毕了。

#### 运行脚本测试：
##### （1）跑测试脚本：
到NS-3对应目录下面执行命令
>sudo ./test.py –c core

跑这个命令可以得到一个非常长的pass过程。
另一种是跑它的hello例程。
>sudo ./waf  --run hello-simulator

可以看到一个“hello simulator”的输出表示执行正确了。
##### （2）另一种检测是否成功的方式
>sudo ./waf --run scratch-simulator
>若没看到任何输出，需要重新配置编译ns-3，输入命令：
>sudo ./waf -d debug --enable-examples --enable-tests configure
>sudo ./waf
>重新运行程序，输入命令：sudo ./waf --run scratch-simulator
>就会看到如下结果：
>Scratch Simulator

至此，我们已经将ns-3网络模拟系统成功安装到自己的计算机里。



## 参考资料
> - [NS-3官网](http://www.nsnam.org/)
> - [Wiki百科](http://www.nsnam.org/wiki/index.php/Main_Page)
