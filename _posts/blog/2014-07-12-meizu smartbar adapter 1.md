---
layout: post
title: 关于魅族SmartBar的适配1
description: 
category: blog
---

+  ####Flyme OS
 
    Flyme OS是魅族公司基于Android4.0系统深度定制的手机操作系统。2009年2月18日魅族推出第一个基于Windows CE6.0内核的正式版本手机操作系统（只适用于魅族M8，称为Mymoblie操作系统），此后推出了为M9及MX深度定制的基于Android 2.2和Android 2.3的操作系统（未正式确立专有名称），但直到2012年6月25日才将为旗下手机基于Android 4.0.3的手机操作系统正式确立为“Flyme”。Eico Design亦参与其设计。此系统最新正式版本为适用于MX3的Flyme 3.0。

+ ####Smartbar

    在 Flyme OS 2.0 中，我们探索出一套兼顾用户界面和操作体验的方案，整合了 Android 操作栏（Action bar）和虚拟导航键，我们称之为 Smartbar。在 Flyme OS 中，遵照 Android 4.0 开发规范设计的应用会自动匹配 Smartbar，并以更具亲和力的方式呈现给用户。如下图：

	![smartbar](http://loo128.github.io/images/meizu smartbar.jpg)

    由上图可以看出Smartbar中可以放置三个东西 返回键、系统菜单键以及Actionbar. 

+ ####适配
    
    首先给大家看一组图片，如下图： 

	![smartbr_no_adapter](http://loo128.github.io/images/smartbr_no_adapter.jpg) 
	![smartbr_adapter](http://loo128.github.io/images/smartbr_adapter.jpg)

 有没有觉得左图下边红色部分放置到最下边smartbar里会好看得多（如右图），而且屏幕的整体面积也变得更大一些，这，就是我们要做的适配

+ Smartbar实现Tab的三种方法
    + 方法一：TabHost+Menu +Activity
    + 方法二：TabHost+Actionbar+Activity
    + 方法三：Actionbar+Fragment

具体实现源码请参照魅族开发者社区发布的Smartbar Demo 里面写的很清楚
下载地址：[http://app.res.meizu.com/fileserver/developdownload/1/11988cc92fa64519867ecd398c8e3c98.rar](http://app.res.meizu.com/fileserver/developdownload/1/11988cc92fa64519867ecd398c8e3c98.rar)

下面我们来分析一下android底部菜单的实现方法，我觉得最核心的是底部菜单的每个主页对应的界面我们是用什么展示的，两种

1. ######Activity 

    这种方式又可以通过两种方式实现各个模块的切换，TabHost 和 ActivityGroup
    可采取上述方法中的方法一和方法二做适配

* ######Fragment  推荐使用

	可采取上述方法中的方法三做适配

######ps：当你使用Actionbar的实现Tab的时候，记住要在Androidmanifest的 application 节点中加上 android:uiOptions="splitActionBarWhenNarrow" 这句话才能让ActionBar显示在底部Smartbar中


   

