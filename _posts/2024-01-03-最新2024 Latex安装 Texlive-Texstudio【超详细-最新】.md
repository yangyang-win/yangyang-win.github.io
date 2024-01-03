---
layout:       post
title: 最新2024 Latex安装 Texlive-Texstudio【超详细-最新】
subtitle: 科研写作神器Latex
date: 2024-01-03 10:44:00 +0800
author:       "Yang"
#categories: [随笔, 年度总结]
tags: 
    - 软件安装
catalog:      true # 是否用目录
header-img:  
header-style:  text # 要不要用图片
header-mask:  # 图片阴暗程度 如果不用图片就设置为0
multilingual: false # 如果为true则会在文章开头显示中英文
mathjax: true # 数学公式？
published: true # 是否展示在页面，为false则完全找不到
hidden: false # 是否展示在主页，不展示在主页在分类里面还可以看见
---
>相信对每个刚迈入科研的小白，latex都是逃不过的工具之一吧。对于研究生来说，使用latex来写论文是非常必需的，不论是发表的小论文，还是编写毕业论文，使用latex来编写论文都是一个非常好的选择。我去年是使用在线编辑器[overleaf](https://www.overleaf.com/)来写的小论文，但是由于在线的编辑器很容易受到网络的影响，于是在新的2024年，我决定弄一个本地的latex编写环境。

我准备使用的latex编写环境是 Texlive 2023 + Texstudio，其中texlive是对latex进行编译的包括一些包、宏什么的，texstudio是latex编辑器，就是一个写作界面。

其中安装顺序推荐先安装 texlive，再安装 texstudio,下面进行安装

### 一、Texlive 2023安装
#### 1、下载Texlive安装包
由于网络的原因，这里推荐使用[清华镜像](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)来下载安装包，选择如下所示的包
![texlive](/_posts/picture/1.png)由于这个包比较大，因此下载的时候可以同时去下载[Texstudio](#二texstudio安装).

#### 2、Texlive安装
##### 2.1 安装包下载完后，打开下载后的安装包，双击运行下图框出的文件进行安装：
![bat](/_posts/picture/2.png)

##### 2.2 刚开始会出现选择安装目录界面，最好是不要安装在C盘
![](/_posts/picture/3.png)

##### 2.3 选择好安装目录后，点击下面的Advanced，然后选择Customize，选择安装的语言包
![](/_posts/picture/4.png)

##### 2.4 默认情况左边的是全选的，我们这里只安装汉语和英语，节省安装空间
![](/_posts/picture/5.png)
![](/_posts/picture/6.png)

##### 2.5 选择好语言包之后，点击安装，然后等待安装好就可以了，可能需要四十分钟
![](/_posts/picture/7.png)

##### 2.6 验证安装是否成功,打开电脑的cmd命令框，输入以下命令：
``` bash
tex -v
```
如果出现类似以下输出则安装成功
![](/_posts/picture/8.png)

### 二、Texstudio安装
#### 2.1 下载Texstudio安装包，点击[官网](https://texstudio.sourceforge.net/)进行下载
![](/_posts/picture/9.png)

#### 2.2 安装，点击下载好的安装包，修改安装目录，最好是不要安装在C盘
![](/_posts/picture/10.png)
选择好安装目录之后，就直接安装，大概需要十分钟

安装好之后直接打开，可以看见直接就是汉语界面，不用再进行设置
![](/_posts/picture/11.png)

下面就可以进行论文写作啦！