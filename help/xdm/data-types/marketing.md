---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；设备；数据类型；数据类型；
solution: Experience Platform
title: 营销数据类型
topic-legacy: overview
description: 本文档概述了Marketing XDM数据类型。
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---


#  Marketingdata类型

 营销是一种标准的XDM数据类型，用于描述与特定接触点活动的营销活动。

![](../images/data-types/marketing.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `campaignGroup` | 字符串 | 营销活动组的名称（如果将多个营销活动分组在一起，如`50%_DISCOUNT`）。 |
| `campaignName` | 字符串 | 营销活动的名称，如`50%_DISCOUNT_USA`或`50%_DISCOUNT_ASIA`。 |
| `trackingCode` | 字符串 | 可用于识别与事件关联的营销活动的跟踪代码。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
