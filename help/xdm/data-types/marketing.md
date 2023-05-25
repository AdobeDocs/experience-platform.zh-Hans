---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；设备；数据类型；数据类型；
solution: Experience Platform
title: 营销数据类型
description: 本文档提供了营销XDM数据类型的概述。
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 3%

---

# [!UICONTROL 营销] 数据类型

[!UICONTROL 营销] 是一个标准XDM数据类型，用于描述对特定接触点有效的营销活动。

![](../images/data-types/marketing.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `campaignGroup` | 字符串 | 营销活动组的名称(在多个营销活动分组的情况下，例如 `50%_DISCOUNT`)。 |
| `campaignName` | 字符串 | 营销活动的名称，如 `50%_DISCOUNT_USA` 或 `50%_DISCOUNT_ASIA`. |
| `trackingCode` | 字符串 | 可用于识别与事件关联的营销活动的跟踪代码。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
