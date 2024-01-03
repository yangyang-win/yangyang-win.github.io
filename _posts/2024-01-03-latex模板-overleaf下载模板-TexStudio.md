---
layout:       post
title: latex模板-overleaf下载模板-TexStudio
subtitle: 使用模板加大写作效率
date: 2024-01-03 17:44:00 +0800
author:       "Yang"
tags: 
    - 论文写作
catalog:      true # 是否用目录
header-img:  
header-style:  text # 要不要用图片
header-mask:  # 图片阴暗程度 如果不用图片就设置为0
multilingual: false # 如果为true则会在文章开头显示中英文
mathjax: true # 数学公式？
published: true # 是否展示在页面，为false则完全找不到
hidden: false # 是否展示在主页，不展示在主页在分类里面还可以看见
---

> 当成功安装了Texlive和TexStudio之后，我们就可以使用TexStudio编辑器来进行写作啦；如果还没有安装Texlive和TexStudio的同学，可以参考之前的博客[Texlive和TexStudio安装](https://blog.csdn.net/qq_51555843/article/details/135357731?spm=1001.2014.3001.5501)

使用TexStudio写作的步骤如下：

1. 新建文档：点击“文件” -> “新建” (英文版 点击 File -> New)
2. 编写论文：在中间的编辑区输入Latex代码
3. 编译：点击 “工具” -> “构建并查看” 进行编译
4. 预览：编译结束之后，TexStudio会自动打开PDF预览，作者可以查看效果。

如果是用Latex写小论文或者毕业论文，可以直接使用对应会议或者期刊的模板，或者学校的Latex模板，在 [overleaf](https://www.overleaf.com/project) 上就有许多模板，我们可以登录overleaf选择我们想要的模板。（注册需要国外的邮箱，如果无法注册的朋友，可以留言你需要的模板，我可以下载下来给你）

我这里使用overleaf来举个例子，采用IEEE会议模板

### 使用Latex模板
#### 1. 进入[overleaf官网](https://www.overleaf.com/project)，点击下图所示的`Templates`
![](/img/in-post/latex-write/1.png)

#### 2. 在搜索栏输入你想下载的模板，我这里搜索IEEE会议模板
![](/img/in-post/latex-write/2.png)

#### 3. 由下图可知，IEEE模板有几个，选择一个最符合你要求的一个，我这里选择的第二个
![](/img/in-post/latex-write/3.png)

#### 4. 这里我们可以直接选择`Open as Template`，它直接在overleaf上以此模板建立一个新project，由于在线overleaf编辑容易受到网络影响，我这里采用的是将模板源码下载到本地使用texstudio编辑，选择`View Source`可以直接下载源码。
![](/img/in-post/latex-write/4.png)

#### 5. 模板源码解读
下载源码解压后，我们会得到如下的文件，其中第一个`conference_101719.pdf`是示例latex代码编译之后生成的pdf，我们可以将其删掉；

第二个`conference_101719.tex`就是主要的latex代码文件了，我们可以按照需要将其修改成我们想要的名字；

第三个`fig1.png`是示例中插入的图片；

第四个`IEEEtran.cls`是一个class文件，它主要是对模板的排版布局进行控制；

第五个`IEEEtran_HOWTO.pdf`是对IEEE会议论文写作的一个说明；其中最重要的就是`.tex`文件，我们主要就是针对这个文件进行论文编写。
![](/img/in-post/latex-write/5.png)

#### 6. 编写论文，使用TexStudio打开刚刚解压得到的模板文件，对`.tex`文件进行编写，编写过程中我们可以编译并且查看pdf，看看是否是我们想要的格式。

### 注：如果无法注册overleaf，可以留言需要的模板