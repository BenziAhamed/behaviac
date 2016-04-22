---
layout: docs_relatives
title: 选择监测节点
date: 2016-02-17 16:46:00 +0800
author: cainhuang
permalink: /docs/zh/references/selectormonitor/
categories: [reference]
lang: zh
---

选择监测节点（SelectorMonitor）和监测分支节点（WithPrecondition）作为对传统行为树的扩展，可以很自然的处理事件和状态的改变。选择监测和监测分支节点只能配对使用，即选择监测节点只能添加监测分支节点作为它的子节点，监测分支节点也只能作为选择监测节点的子节点被添加。

- 选择监测节点是一个动态的选择节点，与选择节点（Selector）相同的是，它选择第一个返回成功的子节点，但不同的是，它不是只选择一次，而是每次执行时都对其子节点重新进行选择。
- 监测分支节点有条件分支子树和动作分支子树。只有条件分支子树返回成功的时候，动作分支子树才能够被执行。

![selectormonitor]({{site.url}}{{site.baseurl}}/img/overview/selectormonitor.png)

图1 选择监测节点和监测分支节点

具体的执行逻辑可以查看[behaviortree/nodes/composites/selectorloop.cpp]({{site.repository}}/blob/master/src/behaviortree/nodes/composites/selectorloop.cpp)

另外，执行行为树的过程中，当状态、条件发生变化或发生事件（Event）时如何响应或打断当前的执行是个重要的问题。

目前behaviac组件支持三种方式来处理状态变化或事件发生：并行节点、选择监测节点、事件附件等。简而言之，并行和选择监测节点的工作方式是采用“轮询”的方式，每次执行时需要重新评估所有子节点，而不是像其他节点会保留上一次正在执行的子节点以便在下一次执行时继续执行。事件附件是在游戏逻辑发出事件时，才按需得到响应。

请详看文档《[事件处理]({{site.url}}{{site.baseurl}}/docs/zh/tutorials/tutorial11_event/)》。