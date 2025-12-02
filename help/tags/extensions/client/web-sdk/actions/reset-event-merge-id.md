---
title: 重置合并ID
description: 已弃用的操作，它允许您分隔同一页面上调用的事件。
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 重置合并ID

>[!IMPORTANT]
>
>此操作已弃用。 请改用[收集内部链接点击次数](../configure/data-collection.md#collect-internal-link-clicks)设置。

**[!UICONTROL Reset merge ID]**&#x200B;操作类型允许您分隔同一页面上调用的事件。 它通常用于内部链接方案，在这些方案中，您可能要将多个负载发送到Adobe。 通过此操作，您可以重置事件的合并ID，以便在它们到达Edge Network后不被视为同一事件的一部分。

如果要控制如何分隔或合并同一页面上的多个事件，请在配置标记扩展时使用[收集内部链接点击量](../configure/data-collection.md#collect-internal-link-clicks)选项。
