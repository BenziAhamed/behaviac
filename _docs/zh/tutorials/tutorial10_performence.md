---
layout: docs_relatives
title: 优化及性能
date: 2015-12-07 10:18:25 +0800
author: cainhuang
permalink: /docs/zh/tutorials/tutorial10_performence/
categories: [tutorial]
lang: zh
---

## 优化及性能
宏BEHAVIAC_RELEASE定义的时候是最终版，BEHAVIAC_RELEASE没有定义的时候是为开发版。开发版下诸如logging，socketing，热加载等开发功能是有效的。

无论是Cpp还是C#版本，`BEHAVIAC_RELEASE`缺省下都是没有定义的。诸如logging，socketing，热加载等开发功能是有效的。
可以通过behaviac::Config::IsLogging和behaviac::Config::IsSocketing来控制是否要Log到文件或是否与编辑器的连接。

<div class="note info">
  <h5>BEHAVIAC_RELEASE缺省下都是没有定义的</h5>
</div>
特别需要指出的是在Cpp的Debug和Release下`BEHAVIAC_RELEASE`缺省下都是没有定义的。

	- 3.2.18版本之前，Release下`BEHAVIAC_RELEASE`缺省的被定义了
	- 3.2.18版本之后，`BEHAVIAC_RELEASE`缺省的都不被定义，Release下也不被定义。


诸如logging，socketing，热加载等开发功能由于有文件操作，运行效率将受到极大的影响，并且在C#下有GC Alloc。可以通过behaviac::Config::IsLogging和behaviac::Config::IsSocketing来控制是否要Log到文件或是否与编辑器的连接。

而当BEHAVIAC_RELEASE定义的时候的最终版里，logging和socketing是关闭的，也不支持连接编辑器。

具体可以参考[开发功能开关]({{site.url}}{{site.baseurl}}/docs/zh/articles/config/)

总之，针对效率可以有下述选择：

 1. 定义`BEHAVIAC_RELEASE`，从而不编译诸如logging，socketing，热加载等开发功能，提供最高效率，也不支持连调功能。
	- C++下，在`config.h`中定义`BEHAVIAC_RELEASE`为1
	- C#下，在Assets目录下的smcs.rsp文件中，定义BEHAVIAC_RELEASE
	- 如果想选择打开或关闭调试功能而不是完全的关闭，则不需要修改任何关于`BEHAVIAC_RELEASE`的定义，通过behaviac::Config::SetLogging和behaviac::Config::SetSocketing来控制是否打开logging和socketing。
 3. 不使用xml或bson格式，而是使用C++或C#格式
 	- C#下，还需要那些在行为树中使用到的Agent的成员都是public的（非public的成员即使通过C#代码访问也需要使用反射系统来进行，会导致GC Alloc以及性能损失）。


<div class="note info">
  <h5>overhead</h5>
</div>
behaviac可以导出xml(bson)，或者源码（cpp/c#），源码的效率要优于数据（xml/bson）的执行效率。实际上这里的效率都是指的behaviac本身的overhead，如果提供的`方法`本身效率很低，运行很慢，behaviac本身的overhead就可以忽略不计了，无论是选用导出何种格式都遇事无补，这个时候，最需要解决的是优化方法的执行效率。

![overhead]({{site.url}}{{site.baseurl}}/img/references/overhead.png)
如上图，尽管xml格式是cpp格式的大约2倍，但这个overhead实际上是非常小的，只有0.0000269秒，0.0269毫秒。（具体数据会因为测试环境的不同有差异）。

