---
title: 医疗保健药物架构字段组
description: 了解医疗保健药物架构字段组。
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# [!UICONTROL 医疗保健药物]架构字段组

[!UICONTROL 医疗保健药物]是[[!UICONTROL 药物]类](../../classes/medication.md)的标准架构字段组。 它提供单个对象类型字段`medication`，用于捕获品牌名称、批号和数量等详细信息。

![](../../images/field-groups/healthcare-medication.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `ingredients` | 对象数组 | 列出药物中的成分。 每个对象都包含以下属性： <ul><li>`isActive`： （布尔值）指示此药物中是否仍在积极使用此成分。</li><li>`name`： （字符串）成分的名称。</li><li>`quantity`： （字符串）药物中存在的配料的数量。</li></ul> |
| `brandName` | 字符串 | 药物的品牌名称。 |
| `codes` | 字符串数组 | 标识此药物的代码列表。 |
| `dosageUnitNumber` | 两次 | 药物的剂量单位编号。 |
| `dosageUnitOfMeasurement` | 字符串 | 剂量数的测量单位。 |
| `expiryDate` | 日期时间 | 药品的有效期。 |
| `genericName` | 字符串 | 药物的通用名称。 |
| `lotNumber` | 字符串 | 药物批次的唯一标识符。 |
| `manufacturerName` | 字符串 | 制药商的名字。 |
| `quantity` | 两次 | 包装里的药量。 |
| `status` | 字符串 | 指示药物/药物是否有效的一般状态。 |
| `volume` | 两次 | 药量。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json)。
