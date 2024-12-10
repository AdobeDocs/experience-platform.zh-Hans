---
title: Money数据类型
description: 了解Money Experience Data Model (XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b910a45-01d5-404b-9710-a2fad9885452
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 18%

---

# [!UICONTROL Money]数据类型

[!UICONTROL Money]是一种标准的体验数据模型(XDM)数据类型，它以某种公认的货币提供了大量的经济效用。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![Money数据类型结构](../../../images/healthcare/data-types/money.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 货币] | `currency` | 字符串 | ISO 4217 货币代码。 |
| [!UICONTROL 值] | `value` | 两次 | 数值。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)
