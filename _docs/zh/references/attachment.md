---
layout: docs_relatives
title: 附件 
date: 2015-12-23 10:06:15 +0800
author: cainhuang
permalink: /docs/zh/references/attachment/
categories: [reference]
lang: zh
---

附件（Attachments）类型可以附加到相应的节点上，在编辑器中有两类附件：显式附件和隐式附件。

## 1 显式附件

显式附件包括前置和后置，如下图所示：

![attachment]({{site.url}}{{site.baseurl}}/img/references/attachment.png)

可以在任何一个节点通过鼠标拖拽来添加前置或后置附件，前置往往是作为前提条件（precondition）来使用，而后置往往是当节点结束的时候施加效果（effect）。

前置的属性主要有“联合”、“执行时机”、“左参数”、“操作符”和“右参数”等，如下图所示：

![attachment]({{site.url}}{{site.baseurl}}/img/references/preaction_prop.png)

其中，“联合”是用于同一个节点的多个前置是“与（and）”还是“或（or）”的运算关系，执行时的逻辑顺序是从上往下依次执行，不管“与”还是“或”。如果“联合”是and
 - 如果有a，b两个前置，则最后的结果是（a and b）。
 - 如果有a，b，c三个前置，则最后的结果是（a and b and c），也即：（（a and b） and c）。如果a是false，b和c还是会计算，没有shortcut的优化。

如果“联合”是or
 - 如果有a，b两个前置，则最后的结果是（a or b）。
 - 如果有a，b，c三个前置，则最后的结果是（a or b or c），也即：（（a or b） or c）。如果a是true，b和c还是会计算，没有shortcut的优化。


“执行时机”分为Enter、Update和Both三种类型：

- Enter表示进入所在节点时，需要检查该前置。

- Update表示所在节点每次更新时，都需要检查该前置。

- Both表示不管所在节点是刚进入还是每次更新时，都需要检查该前置。

后置的属性主要有“执行时机”、“左参数”、“操作符”和“右参数”等，如下图所示：

![attachment]({{site.url}}{{site.baseurl}}/img/references/postaction_prop.png)

“执行时机”分为Success、Failure和Both三种类型：

- Success表示所在节点执行成功后，才需要继续执行该后置。

- Failure表示所在节点执行失败后，才需要继续执行该后置。

- Both表示不管所在节点执行成功还是失败后，都需要继续执行该后置。

## 2 隐式附件

隐式附件主要是指事件这种附件，编辑器中没有单独的事件节点供拖拽来产生，需要通过拖拽另一棵行为树到目标行为树的节点来间接产生该事件附件。

请详看文档《[事件处理]({{site.url}}{{site.baseurl}}/docs/zh/tutorials/tutorial11_event/)》。
