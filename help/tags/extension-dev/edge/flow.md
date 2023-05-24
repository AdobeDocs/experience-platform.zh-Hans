---
title: Edge擴充功能流程
description: 瞭解Adobe Experience Platform中邊緣擴充功能的元件在執行階段如何彼此互動。
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 55%

---

# Edge 扩展流程

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在 Edge 扩展中，每个条件、操作和数据元素类型都有一个允许用户修改设置的视图，以及一个基于用户定义的设置进行操作的库模块。

如下列高階圖表所示，擴充功能的動作型別檢視會顯示於與Adobe Experience Platform整合的應用程式內，呈現於iframe中。 然後使用檢視來修改設定，這些設定會儲存於Platform中。 建置標籤執行階段程式庫時，擴充功能的動作型別程式庫模組以及使用者定義的設定，都會包含在要部署至邊緣節點的執行階段程式庫中。 來自Platform的使用者定義設定會在執行階段插入程式庫模組中。

![扩展流程图](../images/flow/edge/event-processing-flow.png)

在下图中，您可以查看规则处理流程中的事件、条件和操作之间的关联。

![规则处理流程图](../images/flow/edge/rule-processing-flow.png)

规则处理流程包含以下阶段：

1. 启动时，将 `settings` 和 `trigger` 方法提供给事件库模块。
1. 当事件库模块确定事件已发生时，事件库模块调用 `trigger`。
1. Platform 将 `settings` 传递到规则的条件类型库模块中，并在此模块中对条件进行评估。
1. 每个条件类型都会返回条件的值是否为 true。
1. 如果所有条件都评估通过，则执行规则的相应操作。
