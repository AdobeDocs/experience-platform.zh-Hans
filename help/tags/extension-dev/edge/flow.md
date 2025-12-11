---
title: Edge扩展流程
description: 了解Adobe Experience Platform中Edge扩展的组件如何在运行时相互交互。
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 44%

---

# Edge 扩展流程

在 Edge 扩展中，每个条件、操作和数据元素类型都有一个允许用户修改设置的视图，以及一个基于用户定义的设置进行操作的库模块。

如以下高级流程图所示，扩展的操作类型视图显示在与Adobe Experience Platform集成的应用程序的iframe中。 该视图然后用于修改设置，这些设置随后保存在Experience Platform中。 生成标记运行时库后，扩展的操作类型库模块以及用户定义的设置都将包含在要部署到Edge节点的运行时库中。 Experience Platform中的用户定义的设置将在运行时插入库模块。

![扩展流程图](../images/flow/edge/event-processing-flow.png)

在下图中，您可以查看规则处理流程中的事件、条件和操作之间的关联。

![规则处理流程图](../images/flow/edge/rule-processing-flow.png)

规则处理流程包含以下阶段：

1. 启动时，将 `settings` 和 `trigger` 方法提供给事件库模块。
1. 当事件库模块确定事件已发生时，事件库模块调用 `trigger`。
1. Experience Platform将`settings`传递到规则的条件类型库模块中，并在此模块中对条件进行评估。
1. 每个条件类型都会返回条件的值是否为 true。
1. 如果所有条件都评估通过，则执行规则的操作。
