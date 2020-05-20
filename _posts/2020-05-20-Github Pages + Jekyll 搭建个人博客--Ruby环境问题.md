---
layout:     post                    # 使用的布局（不需要改）
title:      Github Pages + Jekyll 搭建个人博客--Ruby环境问题               # 标题 
subtitle:   Ruby环境安装注意事项	#副标题
date:       2020-05-20              # 时间
author:     Kay                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - 环境搭建
---

>   自15年入门开发开始到现在已经有近5个年头了，想写博客的念头已经存在很久了，但是人却一直在犹豫着在哪个平台写比较好。搭建在其他平台s上也总感觉不太靠谱，这阵子终于下定号决心想要在自己服务器上搭建一个，却无奈发现服务器再过一两个月就要过期了。经过这阵子考察，发现可以通过Github Pages + Jekyll 来搭建服务器。
s
博客搭建参考来源（搭建方式和问题解决已经有人写了，大家可以参考下面这两篇文章）：  
[邱柏荧：利用 GitHub Pages 快速搭建个人博客](https://www.jianshu.com/p/e68fba58f75c)（这篇博客主要介绍怎么搭建）  
[张旭（彩云）：GitHub Pages + Jekyll 创建个人博客](https://www.jianshu.com/p/9535334ffd54?appinstall=0)（主要说明遇到问题怎么解决）

本人博客的搭建参考于上面 [@邱柏荧]() 的文章搭建，期间遇到了部分奇奇怪怪的问题（主要是Jekyll版本不一致问题导致的，好在问题都不大，自己通过百度解决），在搭建完后想着我都搭建这么久了，又遇到了这么多问题，要不写个文章记录下吧，防止后来人踏坑。但在查资料时又发现，原来这些问题早有人 [@彩云]() 发现过了。深入对比了下 [@彩云]() 陈列的问题后，发现和我遇到了问题都差不多。

**在此，本片文章就不写搭博客的过程了（有需要参考上面两篇文章即可）**
**本文章只说明几点安装Ruby开发环境 (安装Jekyll前必备的环境) 时遇到的问题**

# 下面简述下我在搭建过程遇到的问题：
#### jekyll环境问题，安装指南请参考：[jekyll官网](https://www.jekyll.com.cn/)
安装Jekyll之前，必须安装好完整的RuBy环境。如下图，通过指令监测到哪个环境不存在，就自己自行百度怎么安装即可（一定要装）。
![Jekyll安装条件](https://upload-images.jianshu.io/upload_images/23466769-f3944c50ee65f11b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
安装时注意下面几点问题：
**1、Ruby的安装目录千万不要有空格（如：Program Files），不然使用时会出问题**
**2、ruby安装好后，顺便修改下ruby的编码(增加两行代码保存即可)，不然后面jekyll本地查看博客文章时，会找不到文件路径，修改方式([Jekyll 解决Jekyll server本地预览文章not found的问题](https://blog.csdn.net/u010632165/article/details/103538062))**
![D:\Ruby26-x64\lib\ruby\2.6.0\webrick\httpservlet\filehandler.rb](https://upload-images.jianshu.io/upload_images/23466769-c144b36e4d28a086.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/550)

**3、GCC的下载时，最好下载编译后的二进制包，然后自己去配置电脑的环境变量就行。如果直接安装GCC，会卡在下载文件的步骤那，而那好像被墙了**








