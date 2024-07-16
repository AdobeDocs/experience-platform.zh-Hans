---
title: 错误详细信息集合数据类型
description: 了解错误详细信息收集Experience Data Model (XDM)数据类型。
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 12%

---

# [!UICONTROL 错误详细信息]集合数据类型

[!UICONTROL 错误详细信息]集合是描述错误详细信息的标准体验数据模型(XDM)数据类型。 使用[!UICONTROL 错误详细信息]集合数据类型捕获错误源和标识的详细信息。 错误ID标识错误，并且错误源指定它来自播放器还是外部源。

![错误详细信息数据类型的图表。](../images/data-types/error-details-collection.png)

| 显示名称 | 属性 | 数据类型 | 必需 | 描述 |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL 错误ID] | `name` | 字符串 | 否 | 错误 ID。 |
| [!UICONTROL 错误Source] | `source` | 字符串 | 否 | 错误源。 已枚举：“player”、“external”以及各自的含义。 |

{style="table-layout:auto"}
