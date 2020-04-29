---
title: Hexo+GitHub博客搭建教程
toc: true
tags: 博客
categories: '学习拓展'
abbrlink: 44464
date: 2020-04-03 19:18:19
---

## 背景介绍

博客搭建是最近完成的，赶在还没忘记部署内容尽快记录下来。

我选取的Hexo架构搭建博客，Hexo是一个专门针对博客的框架，它简洁快速，容易部署在GitHub和Coding平台。它的官方网站[Hexo官方网站](https://hexo.io/zh-cn/index.html)有关于它的简单介绍，它的优势在于速度快、支持Markdown语法，可以轻松部署在Github、Heroku、Coding等等平台，而且可以通过安装多个插件来增加多样的功能。

Hexo的安装依赖于GitHub网页，程序员朋友对GitHub会比较熟悉，因为常用来做版本管理，觉得陌生的朋友也没有关系，我们不需要对它的操作非常了解，因为只会用到非常少的一部分功能。GitHub Page搭建服务器免费方便，但是有时需要“科学的上网方式”，访问速度有点慢，我觉得可以接受嗷，觉得无法接受的朋友可以换一个平台看看。

## 准备工作

准备工作比较简单，这边只做一个列举，不知道你们到哪一步的可以看着来：

* 拥有GitHub账号，没有就注册。注册网站[GitHub官网](https://github.com/)，按照提示步骤一一完成即可。
* 本机电脑安装Git，根据自己的电脑选择客户端。参考链接[安装Git]([https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git](https://git-scm.com/book/zh/v2/起步-安装-Git))。安装好Git之后，有命令行使用经验的朋友可以很快上手，它和Linux命令行操作基本相同，你甚至可以把它当作terminal来使用，非常强悍和方便。

  ![安装Git介绍.png](https://s1.ax1x.com/2020/04/03/GayhSP.png)
* 本机电脑安装npm和node.js，npm是包管理，node.js是对Hexo的环境支持。你可以打开电脑的powershell或者terminal来进行安装。要注意npm基于node.js，所以你必须先安装node.js，node直接到官网下载傻瓜式安装即可。

![node安装.png](https://s1.ax1x.com/2020/04/03/Ga6R74.png)

安装完node.js后再命令行输入命令即可安装npm：

```
// 安装指定版本
npm install npm @版本号
// 安装最新版本
npm install npm @latest -g
// 安装报错，提示用root权限去执行，可以执行
sudo npm install npm @latest -g
// 安装下一个未发布的npm版本
npm install npm@next -g
```

再powershell或者terminal种检查安装：

![检查安装.png](https://s1.ax1x.com/2020/04/03/Gac2xP.png)

当命令行返回版本号说明安装成功。

以上，准备工作完成。

## 开始部署

### 创建GitHub仓库

在GitHub官网界面，找到这个New按钮：

![创建博客.png](https://s1.ax1x.com/2020/04/03/Gagixx.png)

建立一个名为“GitHub用户名.github.io”的仓库，用户名换成自己的用户名，比如我的：

![OzwardPenrose建立仓库.png](https://s1.ax1x.com/2020/04/03/GagJeS.png)

一定要是这个命名规则！不然不能生效。这个仓库名也就是后面我们访问自己的博客的地址了，如果你有自己的域名还可以绑定一下，这里不介绍了。

### 设置SSH

我们需要使用SSH连接来解决本地和服务器端的连接问题，打开Git，Git是一个类似terminal的终端页面。

在资源管理器右键git bash here就可以打开，然后输入命令：

```
ssh-keygen -t rsa -C "邮件地址"
```

邮件地址就是你的GitHub注册邮箱。

连续几次回车后，到C:/user/windows用户名的目录下面找到一个“.ssh”的文件夹，打开id_rsa.pub，复制。

进入GitHub，在自己的设置界面找到“SSH and GPG keys”这一栏

![增加SSH key.png](https://s1.ax1x.com/2020/04/04/GdLp4I.png)

选钟 New SSH key。

![SSH key.png](https://s1.ax1x.com/2020/04/04/GdLCCt.png)

将你刚刚复制的SSH粘贴进去。

然后测试一下是否成功：

```
$ ssh -T git@github.com # 注意邮箱地址不用改
```

如果回复你：

Hi “用户名”! You’ve successfully authenticated, but GitHub does not provide shell access.

就说明SSH设置已经成功。

你还需要输入以下两条命令：

```
git config --global user.name "用户名"
git config --global user.email "邮箱地址"
```

### 配置本地hexo

本地新建一个文件夹用于放置你所有的博客相关的文件，我将它命名为Blog，后面就直接用Blog来称呼。

#### 安装hexo

在文件夹右键Git bash here，输入命令

```
npm install hexo-cli -g
```

#### 初始化hexo

在git种继续输入初始化命令

```
hexo init
```

这个命令执行完毕后，会发现文件夹多了一些东西，这就是我们博客的配置文件了，以后对博客网站的修改更新都要通过这些文件。

可以试试看是否生成成功，git输入两行命令：

```
hexo g # 生成
hexo s # 启动服务
```

然后可以看看网站[http://localhost:4000](http://localhost:4000)，是否能正常本地访问hexo网页，其效果应该是这样的：

![Hexo的网页.png](https://s1.ax1x.com/2020/04/04/GwmJ5n.png)

看到这个界面，说明本地部署已经完毕了。

#### 修改主题

默认的Hexo主题不太好看，我们可以自己选择一个比较合适的主题，Hexo有一个主题库：[https://hexo.io/themes/](https://hexo.io/themes/)

![hexo主题库.png](https://s1.ax1x.com/2020/04/04/GwQhEF.png)

依照自己喜欢的选定并下载到Blog的theme文件夹下，然后在Blog文件夹的__config.yml文件种修改。

#### 修改_config.yml文件

Blog文件夹下的config是对博客基本设置的内容，包括一些网站名字之类的内容，具体的说明可以参考它的介绍网站[hexo的config.yml](https://hexo.io/docs/configuration.html)。

要注意我们需要修改的一个重要部分就是关于网站的设置，我们需要把它和我们部署在GitHub的内容相连：

![修改url.png](https://s1.ax1x.com/2020/04/04/GwGKFU.png)

![修改deploy.png](https://s1.ax1x.com/2020/04/04/Gw27ut.png)

马赛克的部分就是你的Github用户名。这个部分的修改是你的博客能顺利部署在Github上的基础，其他的修改可以按照自己的喜好。

除了Blog根目录下的config还有theme的config，这个config的修改并没有定式，可以先按照主题在Github的markdown文件进行修改，想要加其他功能都可以加。这部分的呢欧容可以参考个人博客优化的文章。

### 上传到GitHub

上传到Github反而是最简单的一步了，在此之前你要先安装一个部署插件：

```
npm install hexo-deployer-git --save
```

然后执行命令：

```
//清除预览
hexo clean
//部署
hexo generate
hexo deploy
```

后两条命令可以直接写成“hexo g -d”。

此时你就可以通过[https://你的Github用户名.github.io]访问你的个人博客了。

### 开始写作

博客网站部署完毕就可以持续写自己的文章了，Hexo在部署上的方便性非常适合用于博客。比如我们新建一个博客文章，只要在git输入：

```
hexo new "aticle title"
```

然后可以在/Blog/source/_post目录下看到一个命名为“article title”的markdown文件，用电脑的markdown编辑器打开就可以了，推荐使用Typora。

写完文章后保存，在git输入部署时的三条命令即可。

至此完成基础搭建，感谢各位。

## 参考资料

> - [免费个人博客：使用hexo+github搭建详细教程](https://blog.csdn.net/xun527/article/details/104756517/)
> - [Hexo + GitHub 搭建个人博客](https://hacpai.com/article/1565759431848)
