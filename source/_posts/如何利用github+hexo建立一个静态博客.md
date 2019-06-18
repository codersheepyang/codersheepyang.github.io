---
layout: post
title:  如何利用github+hexo建立一个静态博客
tags:
	- hexo
categories:
	- site
date:  2019-02-23 4:38
description: 这篇博文讲述hexo博客网站创建的大致流程
---
##### 一、先说说为什么会建立这个博客：
&emsp;&emsp;首先我是在一次偶然的机会在b站看到了一个程序员up主codersheep（up id:CoderSheep），然后发现up主干货满满，其中有一个视频教程《程序猿如何搭建一个属于自己的个人博客》（视频路径：[点击](https://www.bilibili.com/video/av37128014)），才发现原来一个静态博客是如此好搭，只需要完全跟着教程，部署环境、找模板、上传模板、最后链接服务器，就完全ok了。因为在这之前我是有考虑自己搭一个动态博客的，但由于我的技术栈是完全偏向后端的，虽说前端模板，但是还是会有改动的地方，但是由于我的前端水平...最后改动的一团糟，而且主页和博客页是是完全两种画风，导致最后我放弃了。而今发现原来静态博客是如此简易好搭还完全不需技术考虑，所以就慢慢跟着各种博文搭建大概2天（在很慢的情况下），也比较美观简易，唯一不好的是访问比较慢，网站资源少还稍微快一点，如果搭建的网站上存在图片，甚至视频时，那如果是在没缓存的情况下访问时会是相当慢的...因为这个静态博客是放在github的服务器上的，根本没有做cdn加速这些，但是要是自己平时写写博客那就够用了。其次我建立博客的初衷是为了能写一点自己学的技术的一些想法和拓展，因为之前用博客园写了好多学习笔记...虽然学习笔记也是博客的一种承载形式，但是现在更多的是想在有一定技术支持的基础上，能够拓展出不一样的东西。
##### 二、搭建博客流程：
###### 1.环境搭建：
&emsp;&emsp;需要工具：node.js（hexo需要node.js的支持）,git（上传工具），github(服务器)。
&emsp;&emsp;1.git下载：
&emsp;&emsp;[点击](https://gitforwindows.org/)（在没有翻墙的情况下，下载速度比较慢，可以尝试到其他地方找找资源），顺序安装即可。
&emsp;&emsp;2.node下载：
&emsp;&emsp;[点击](https://nodejs.org/en/)，顺序安装即可。
&emsp;&emsp;3.hexo下载：
&emsp;&emsp;在下载hexo之前，需要先创建一个hexo文件夹，用于后期存放所创建的博客文件。如果已经下载好的git之后，在桌面右击，会出现Git Bash Here的按钮，然后点击进入。在窗口输入：
&emsp;&emsp;npm install hexo-cli -g
&emsp;&emsp;然后输入：
&emsp;&emsp;npm install hexo --save
&emsp;&emsp;安装完成后，可查看版本：
&emsp;&emsp;hexo -v
&emsp;&emsp;执行init命令对hexo进行初始化操作：
&emsp;&emsp;hexo init
&emsp;&emsp;上面的步骤就完成了环境的搭建。
###### 2.服务测试：
&emsp;&emsp;hexo generate（生成静态文件） - 缩写： hexo g
&emsp;&emsp;hexo server (启动服务器) - 缩写：hexo s
&emsp;&emsp;本地访问：localhost:4000/.如果显示出来hexo的主页，那么说明环境部署成功。
###### 3.搭建github环境：
&emsp;&emsp;1.首先需要创建一个属于自己的github账号：[地址](github.com)。
&emsp;&emsp;2.点击+号选择New repository 新创建一个仓库。在这对Resitory name有严格的要求，必须和owner的名字一致。例如：owner名字如果是codersheepyang，那么后面的名字就需要是codersheepyang.github.io，然后点击create repository一个新仓库就创建好了。
&emsp;&emsp;3.开启GitHub pages
&emsp;&emsp;打开所创建库的setting页面，找到GitHub Pages，创建即可，创建成功后，便可以通过浏览器访问owner.github.io。

###### 4.连接本地hexo和github：
&emsp;&emsp;1.配置git个人信息：
&emsp;&emsp;①git config --system user.name "yourusername"
&emsp;&emsp;②git config --system user.email "youremail@163.com"
&emsp;&emsp;2.修改_config.yml的部分配置：
&emsp;&emsp;可以依照自己喜欢的风格对配置进行修改，可参考hexo的官方文档。目前主要是修改以下配置来做两者的连接：
&emsp;&emsp;Deployment部分：
&emsp;&emsp;deploy:
&emsp;&emsp;type: git
&emsp;&emsp;repo: git@github.com:codersheepyang/codersheepyang.github.io.git
&emsp;&emsp;branch：master(master作为默认分支，如需自己创建分支作为主分支修改此部分)
&emsp;&emsp;注意：在每个冒号后面都需要添加一个空格，要不然会对文件格式解析错误。
&emsp;&emsp;3.发布:
&emsp;&emsp;这需要以后在操作博客的三个常用指令：
&emsp;&emsp;①hexo clean（清除缓存文件（db.json）和已经生成的静态文件（public）。在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令）
&emsp;&emsp;②hexo g（上面已说过）
&emsp;&emsp;③hexo d（部署网站）
&emsp;&emsp;配置ssh key：
&emsp;&emsp;好处:由于git使用https协议，所以在每次pull、push的时候都需要输入密码，使用git协议，使用ssh密钥，可以省去每次输入密码。
&emsp;&emsp;本机ssh公钥存放在本机主目录的~/.ssh目录下。可以使用cd ~/.ssh 访问，如果存在此文件，那么密钥就在id_rsa.pub文件下。(如果不存在ssh文件的话使用 ssh-keygen -t rsa -C "your_email@youremail.com" 命令创建即可)，然后进入github的settings，找到SSH and GPG keys,添加刚复制的内容即可。
###### 5.选择主题
&emsp;&emsp;1.下载主题
&emsp;&emsp;上面步骤完成之后那么说明整个博客的环境+搭建已经完成。现在就是对博客的美化阶段，你可以在hexo的官方找一个你喜欢的主题，然后进入该主题的github页面，选择Clone or download复制链接。然后在git bash界面进入安装hexo时的them路径。输入指令git clone yourcopypath。下载完成后主题就在theme文件夹里面了。
&emsp;&emsp;2.配置主题：
&emsp;&emsp;进入_config.yml文件：
&emsp;&emsp;找到theme
&emsp;&emsp;theme: 主题名(这是下载主题的文件名)，然后再输入 hexo clean、hexo g 、hexo d这三个命令即可更新线上的数据。再次打开就会显示新主题主页。
##### 三、搭建后的想法
&emsp;&emsp;看似简短的几个步骤我却用了大概10个小时才完成所有流程...因为遇到了太多的问题了，最开始教程使用不当带来的指令顺序问题，然后是npm包版本依赖问题(中途自己猪修改文件名导致)，ssh key找不到的问题等等，所以再简单的东西都需要仔细的了解每一个步骤然后再进行实际的操作，要不然云里雾里都不知道自己在干什么，这样即使完成了也收获不了什么，所以以后做事一定要更仔细认真~
			

