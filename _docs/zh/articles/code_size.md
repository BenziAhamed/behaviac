---
layout: docs_relatives
title: Cpp生成代码大小的说明
date: 2016-04-27 11:16:00 +0800
author: jonygli
permalink: /docs/zh/articles/code_size/
categories: [doc]
lang: zh
---

Cpp版本广泛的用到了template。

>Code bloat occurs because compilers generate code for all templated functions in each translation unit that use them. Back in the day the duplicate code was not consolidated resulting in "code bloat". These days the duplicate code can be removed at link time.

所以，在看到产生的代码的大小后不要过于惊慌。（另外，编译速度也会比较慢。）

在3.4.0后的版本里，behaviac已经支持了Link Time Optimization（LTO）。LTO可以极大的减少产生代码的大小以及优化产生代码的效率。

### gcc

 - 如下所示，通过参数指定`Release`以及`ForeUseRelease`可以打开LTO（如果你的gcc支持的话）
`cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release -DBEHAVIAC_VERSION_MODE=ForeUseRelease --build ../../../..`
 - 或者通过cmake gui设置`CMAKE_BUILD_TYPE`为`Release`和`BEHAVIAC_VERSION_MODE`为`ForeUseRelease`
 - gcc版本需要是4.9以上，低版本不支持LTO
 - 其他版本的gcc请参考相应文档设置LTO

### msvc

 - 在visual studio中可以参考打开编译选项/Gy及/OPT:ICF /OPT:REF /LTCG链接选项
 - 指定`ForeUseRelease`的时候，cmake生成的项目文件，在Release下缺省的已经打开上述优化开关。
 - 也可以考虑调整O1,O2或Ox编译选项

