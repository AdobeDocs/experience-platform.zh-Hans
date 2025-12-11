---
title: Web扩展流程
description: 了解Web扩展组件如何在Adobe Experience Platform中在运行时相互交互。
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 47%

---

# Web 扩展流程

在 Web 扩展中，每个事件、条件、操作和数据元素类型都有一个允许用户修改设置的视图，以及一个基于用户定义的这些设置进行操作的库模块。

如以下概要流程图所示，扩展的事件类型视图将显示在与Adobe Experience Platform集成的应用程序的iframe中。 然后，用户使用该视图来修改设置，这些设置随后保存在Experience Platform中。 生成标记运行时库后，扩展的事件类型库模块以及用户定义的设置都将包含在运行时库中。 运行时，Experience Platform会将用户定义的设置注入库模块。

![扩展流程图](../images/flow/web/extension-flow.png)

在下图中，您可以查看规则处理流程中的事件、条件和操作之间的关联。

![规则处理流程图](../images/flow/web/rule-processing-flow.png)

规则处理流程包含以下阶段：

1. 启动时，将 `settings` 和 `trigger` 方法提供给事件库模块。
1. 当事件库模块确定事件已发生时，事件库模块调用 `trigger`。
1. 标记将`settings`传递到规则的条件库模块中，并在此模块中对条件进行评估。
1. 每个条件库模块返回条件的值是否为 true。
1. 如果所有条件都评估通过，则执行规则的操作。
