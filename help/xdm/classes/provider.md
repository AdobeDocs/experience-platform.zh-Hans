---
title: 提供程序类
description: 本文档概述了Experience Data Model(XDM)中的Provider类。
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 4%

---

# [!UICONTROL 提供程序] 类

在Experience Data Model(XDM)中， [!UICONTROL 提供程序] 类可捕获定义提供商业务实体（例如医疗保健提供商或保险提供商）的最小属性集。

![类结构](../images/classes/provider.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `providerName` | [[!UICONTROL 人员姓名]](../data-types/person-name.md) | 提供商的名称。 |
| `_id` | [!UICONTROL 字符串] | 记录的唯一、系统生成的字符串标识符。 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会为其提供显式值。 但是，如果您愿意，您仍可以选择提供您自己的唯一ID值。 |
| `providerId` | [!UICONTROL 字符串] | 提供程序的唯一标识符。 |

{style=&quot;table-layout:auto&quot;}

类可以使用 [[!UICONTROL 医疗保健提供商] 字段组](../field-groups/provider/healthcare-provider.md) 以详细描述医疗保健提供商。
