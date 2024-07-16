---
title: 提供程序类
description: 了解Experience Data Model (XDM)中的Provider类。
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL 提供程序]类

在Experience Data Model (XDM)中，[!UICONTROL Provider]类捕获定义提供商业务实体（如医疗保健提供商或保险提供商）的最小属性集。

![类结构](../images/classes/provider.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `providerName` | [[!UICONTROL 人员姓名]](../data-types/person-name.md) | 提供程序的名称。 |
| `_id` | [!UICONTROL 字符串] | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。 |
| `providerId` | [!UICONTROL 字符串] | 提供商的唯一标识符。 |

{style="table-layout:auto"}

可以使用[[!UICONTROL 医疗保健提供商]字段组](../field-groups/provider/healthcare-provider.md)扩展该类，以描述有关医疗保健提供商的更多详细信息。
