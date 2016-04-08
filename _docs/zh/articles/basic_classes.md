---
layout: docs_relatives
title: 运行时端常用类的介绍
date: 2016-04-05 15:33:31 +0800
author: cainhuang
permalink: /docs/zh/articles/basic_classes/
categories: [doc]
lang: zh
---

在使用behaviac运行时端（Runtime）的源代码或API时，有几个最常用的类值得注意：如Workspace、Agent、Config等。

### Workspace类

Workspace类主要用于管理元信息的导出，加载、卸载、执行、停止执行行为树，设置时间和帧数等。

- GetInstance() ：用于获取Workspace的单件实例。

- ExportMetas(const char*) ：导出元信息文件到指定的路径，详见文档《[C++运行时端中元信息的注册和导出]({{site.url}}{{site.baseurl}}/docs/zh/tutorials/tutorial3_1_meta_cpp_register/)》。

- SetFilePath(const char*) ：用于加载行为树时指定行为树文件所在的目录。

- SetFileFormat(EFileFormat) ：用于指定加载行为树文件的格式，包括Xml、Bson、Cpp/Cs、Default。其中Default表示先尝试加载Xml格式，如果找不到再尝试加载Bson格式，最后尝试加载Cpp/Cs格式，这个功能可用于行为树的热更新。

- Update() ：用于执行所有Agent的当前行为树，行为树的执行也可以不通过该API，可以自己单独调用Agent的btexec()方法，详见文档《[运行时端的更新流程]({{site.url}}{{site.baseurl}}/docs/zh/tutorials/tutorial13_updateloop/)》。

- DebugUpdate() ：用于执行调试和热加载相关的方法，如果已经使用了Update()方法来执行，则连调或热加载时就不需要再调用该DebugUpdate()方法。

- SetIsExecAgents(bool) ：用于停止/继续执行所有Agent的当前行为树，前提是行为树是执行是通过Update()方法发起的。如果是自己单独调用Agent的btexec()方法，则通过Agent的SetActive(bool)方法来停止/继续执行。

- SetTimeSinceStartup(double) ：用于设置游戏从启动到当前的总时间，该总时间主要用于时间、等待时间等与时间有关的节点的执行。如果不每帧设置该值，这些节点将不会正常工作。

- SetFrameSinceStartup(int) ：用于设置游戏从启动到当前的总帧数，该总帧数主要用于帧数、等待帧数等与帧数有关的节点的执行。如果不每帧设置该值，这些节点将不会正常工作。

具体的代码可以查看[behaviac/base/workspace.h]({{site.repository}}/blob/master/inc/behaviac/base/workspace.h)

### Agent类

静态方法：

- Create(const char*, int, short) ：用于创建Agent的实例。

- Destroy(Agent*) ：用于销毁Agent的实例。

- Register() ：注册该Agent类，用于记录该类的元信息。

- UnRegister() ：取消注册该Agent类。

- RegisterInstanceName(const char*, const wchar_t*, const wchar_t*) ：注册实例名字，作为元信息的一部分，导出后可用于编辑器中节点的配置。

- UnRegisterInstanceName(const char*) ：取消注册实例名字。

- BindInstance(Agent*, const char*, int) ：将某个Agent实例跟某个名字进行绑定。

- UnbindInstance(const char*, int） ：取消某个Agent实例跟某个名字的绑定。

成员方法：

- btload(const char*, bool) ：用于加载指定名字的行为树，不需要后缀名（文件格式）。

- btunload(const char*) ：用于卸载指定名字的行为树。

- btsetcurrent(const char*) ：用于设置当前行为树。

- btexec() ：执行当前行为树。

- SetActive(bool) ：用于停止/继续执行当前行为树，如果设置为false，表示停止执行当前行为树；否则，表示继续执行。

- FireEvent(const char*) ：用于发出事件，以便于行为树中绑定的事件得到响应。

- SetIdFlag(uint32_t) ：用于设置连调时是否需要跟踪该Agent。通过静态方法SetIdMask()设置全部Agent的Mask值，然后再通过SetIdFlag()设置当前Agent的Flag值。如果IsMasked()返回为真，则表明需要跟踪该Agent。

- SetName(const char*) ：用于设置名字。

具体的代码可以查看[behaviac/agent/agent.h]({{site.repository}}/blob/master/inc/behaviac/agent/agent.h)

### Config类

详见文档《[开发功能开关]({{site.url}}{{site.baseurl}}/docs/zh/articles/config/)》。
