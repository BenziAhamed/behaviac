---
layout: docs_relatives
title: 并行节点 
date: 2015-12-13 13:26:15 +0800
author: jonygli
permalink: /docs/zh/references/parallel/
categories: [reference]
lang: zh
---

![parallel]({{site.url}}{{site.baseurl}}/img/references/parallel.png)

Parallel 节点在最一般意义上是并行的执行其子节点，“一边做A，一边做B”。 在 Selector 和 Sequence 中，‘顺序’的‘ 一个一个’ 的执行子节点， 上一个子节点执行结束后， 根据其状态是否执行接下来的子节点。 Parallel 节点在逻辑上是‘同时’并行的执行所有子节点，然后根据所有子节点的状态决定本身的状态。 如何根据所有子节点的状态决定本身的状态呢？具体的如下图， Parallel节点有几个属性可以配置：

![parallelproperties]({{site.url}}{{site.baseurl}}/img/references/parallelproperties.png)

 - 失败条件， 决定 Parallel 节点在什么条件下是失败的
 - 成功条件，决定 Parallel 节点在什么条件下是成功的
 - 子节点结束继续条件，子节点结束后是重新再循环执行还是结束后不再执行
 - 退出行为， 当 Parall 节点的成功条件或失败条件满足而成功或失败后， 是否需要 abort掉其他还在运行的子节点
 - 当子节点执行状态既不满足失败条件，也不满足成功条件，且无 Running 状态子节点时，Parallel 节点返回 Failure

在序列 Sequence 中，当条件节点之后跟着其他节点的时候，条件节点实际上是作为其他节点的 precondition，只有条件节点是 true，下面的其他节点才有可能执行。
Parallel 节点可以用来实现所谓‘ context precondition’，如下图：

![parallel_condition]({{site.url}}{{site.baseurl}}/img/references/parallel_condition.png)

Parallel 节点配置条件节点和其他节点， 并且失败条件是缺省的配置 FAIL_ON_ONE ，那么只有当条件节点成功的时候其他节点才被执行，从而条件节点事实上是其他节点的precondtion。 （但是需要特别指出的是，作为precondition的这种用法是不严谨的，当条件失败的时候，在Parallel失败之前，后续的节点会多执行一次。请使用前置附件来实现这种precondition的需求）


和 Sequence 的不同之处在于， Sequence 节点实现的 precondition 只是‘进入’其他节点的 precondition，一旦‘进入’开始执行其他节点就不再检查该 precondition 了，而 Parallel 节点实现的 precondition 是‘ context’的，不但‘进入’开始执行前需要检查，之后每次执行也都要检查。

具体的执行逻辑可以查看 [behaviortree/nodes/composites/parallel.cpp]({{site.repository}}/blob/master/src/behaviortree/nodes/composites/parallel.cpp)