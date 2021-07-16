---
title: 边缘扩展流量
description: 了解Adobe Experience Platform中边缘扩展的组件在运行时如何彼此交互。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 46%

---

# Edge 扩展流程

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

在 Edge 扩展中，每个条件、操作和数据元素类型都有一个允许用户修改设置的视图，以及一个基于用户定义的设置进行操作的库模块。

如以下概要图所示，扩展的操作类型视图显示在与Adobe Experience Platform集成的应用程序的iframe中。 然后，将使用视图来修改设置，这些设置随后将保存在Platform中。 构建标记运行时库后，扩展的操作类型库模块以及用户定义的设置都将包含在将部署到边缘节点的运行时库中。 运行时，来自平台的用户定义的设置将插入到库模块中。

![扩展流程图](../images/flow/edge/event-processing-flow.png)

在下图中，您可以查看规则处理流程中的事件、条件和操作之间的关联。

![规则处理流程图](../images/flow/edge/rule-processing-flow.png)

规则处理流程包含以下阶段：

1. 启动时，将 `settings` 和 `trigger` 方法提供给事件库模块。
1. 当事件库模块确定事件已发生时，事件库模块调用 `trigger`。
1. Platform 将 `settings` 传递到规则的条件类型库模块中，并在此模块中对条件进行评估。
1. 每个条件类型都会返回条件的值是否为 true。
1. 如果所有条件都评估通过，则执行规则的相应操作。
