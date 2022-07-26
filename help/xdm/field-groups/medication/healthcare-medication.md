---
title: 医疗保健药物方案字段组
description: 本文档概述了医疗保健药物架构字段组。
source-git-commit: 3b0c85eb5184dd116b1013e617cf528080fa0656
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 6%

---

# [!UICONTROL 一种保健药物] 架构字段组

[!UICONTROL 一种保健药物] 是的标准架构字段组 [[!UICONTROL 药物] 类](../../classes/medication.md). 它提供单个对象类型字段 `medication` ，可捕获品牌名称、批号和数量等详细信息。

![](../../images/field-groups/healthcare-medication.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `ingredients` | 对象数组 | 列出药物中存在的成分。 每个对象包含以下属性： <ul><li>`isActive`:（布尔值）指示此药物中是否仍在积极使用此成分。</li><li>`name`:（字符串）配料的名称。</li><li>`quantity`:（字符串）药物中存在的成分的数量。</li></ul> |
| `brandName` | 字符串 | 药品的品牌名称。 |
| `codes` | 字符串数组 | 标识这种药物的代码列表。 |
| `dosageUnitNumber` | 双精度 | 药物的剂量单位号。 |
| `dosageUnitOfMeasurement` | 字符串 | 剂量数的测量单位。 |
| `expiryDate` | DateTime | 药物的到期日。 |
| `genericName` | 字符串 | 药物的通用名称。 |
| `lotNumber` | 字符串 | 药品批次的唯一标识符。 |
| `manufacturerName` | 字符串 | 药厂的名字。 |
| `quantity` | 双精度 | 包装中的药量。 |
| `status` | 字符串 | 一般状态，指示药物/药物是否有效。 |
| `volume` | 双精度 | 药的体积。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
