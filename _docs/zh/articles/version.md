---
layout: docs_relatives
title: 版本号说明
date: 2016-04-15 10:16:00 +0800
author: jonygli
permalink: /docs/zh/articles/version/
categories: [doc]
lang: zh
---

在源码和安装包的根目录都提供了[version.txt]({{site.repository}}/blob/master/version.txt)。unity的源码里也提供了[version.txt]({{site.repository}}/blob/master/integration/unity/Assets/Scripts/behaviac/runtime/version.txt)。

 1. version.txt中的版本号和安装包（如BehaviacSetup_3.3.16.exe）的版本号以及编辑器的版本号是一致的。请使用相同版本号的编辑器，运行时。
 1. version.txt的存在是用来表明该版本的版本号之用。出现了问题请提供该版本号。
 1. version.txt只是从3.3.16版本后才提供。之前的版本中没有改文件。
 1. Cpp版本中提供了函数`behaviac::GetVersionString()`来返回版本号，该版本号和version.txt中的版本号是一致的。
 1. Cpp版本运行的时候，有下图所示的信息。
 ![cppinfo]({{site.url}}{{site.baseurl}}/img/articles/cppinfo.png)
    - 第一行就包含了版本信息。其中的debug，NRELEASE等信息是用来表明是否定义了宏`_DEBUG`或`DEBUG`,`BEHAVIAC_RELEASE`
    - 该信息在vs的输出窗口中有输出，在`_behaviac_$_$_.log`文件里也有输出。
