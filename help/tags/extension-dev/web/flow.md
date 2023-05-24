---
title: Web擴充功能流程
description: 瞭解Web擴充功能元件如何在執行階段在Adobe Experience Platform中互相互動。
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 57%

---

# Web 扩展流程

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在 Web 扩展中，每个事件、条件、操作和数据元素类型都有一个允许用户修改设置的视图，以及一个基于用户定义的这些设置进行操作的库模块。

如下列高階圖表所示，擴充功能的事件型別檢視會顯示於與Adobe Experience Platform整合的應用程式內，呈現於iframe中。 然後，使用者會使用檢視來修改設定，然後這些設定會儲存在Platform中。 建置標籤執行階段程式庫時，擴充功能的事件型別程式庫模組以及使用者定義的設定都會包含在執行階段程式庫中。 运行时，Platform 会将用户定义的设置注入库模块。

![扩展流程图](../images/flow/web/extension-flow.png)

在下图中，您可以查看规则处理流程中的事件、条件和操作之间的关联。

![规则处理流程图](../images/flow/web/rule-processing-flow.png)

规则处理流程包含以下阶段：

1. 启动时，将 `settings` 和 `trigger` 方法提供给事件库模块。
1. 当事件库模块确定事件已发生时，事件库模块调用 `trigger`。
1. 標籤路徑 `settings` 放入規則的條件程式庫模組中，以評估條件。
1. 每个条件库模块返回条件的值是否为 true。
1. 如果所有条件都评估通过，则执行规则操作。
