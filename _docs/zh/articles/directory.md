---
layout: docs_relatives
title: 目录结构
date: 2016-03-29 10:26:13 +0800
author: jonygli
permalink: /docs/zh/articles/directory/
categories: [doc]
lang: zh
---

首先说明的是从[下载](https://github.com/TencentOpen/behaviac/releases)下载的BehaviacSetup*.exe是安装包，内含可执行的编辑器及示例。

可能需要下载安装[Microsoft Visual C++ 运行库](https://support.microsoft.com/en-us/kb/2977003)。
及[.net](https://www.microsoft.com/en-US/download/details.aspx?id=21)。

https://www.microsoft.com/en-us/download/details.aspx?id=40784

这里介绍的是源码的目录结构。从[github](https://github.com/TencentOpen/behaviac)下载或克隆源码。

## 目录结构图示：

 ![directory]({{site.url}}{{site.baseurl}}/img/articles/directory.png)

## 目录结构说明
  - build，构建脚本，可以参考[构建]({{site.url}}{{site.baseurl}}/docs/zh/articles/build/)
  - docs, 文档，目前只有behaviac.chm，以后访问文档需要访问[API](http://www.behaviac.com/)
  - example，示例
    - airbattledemo，cocos2d-x的示例，C++
    - spaceship，SDL的示例，C++
  - inc，c++的包含include文件
  - integration，unity平台的实现及示例
    - BattleCityDemo，unity 示例
    - unity，unity的实现及unittest
  - src，c++源码
  - test，测试，C++
    - btperformance，简单的性能测试
    - btremotetest, 简单的连调测试
    - btunittest, C++ unittest
    - demo_running, 简单的测试，适合少量修改，体会[行为树的概念](http://www.behaviac.com/docs/zh/articles/concepts/)
    - usertest, 简单的测试，适合少量修改，做出自己的测试