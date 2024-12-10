---
title: 比率数据类型
description: 了解比率体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL 比率]数据类型

[!UICONTROL Ratio]是标准的体验数据模型(XDM)数据类型，通过分子和分母提供两个[[!UICONTROL 数量]](../data-types/quantity.md)值的比率。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![比率数据类型结构](../../../images/healthcare/data-types/ratio.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 分母] | `denominator` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 分母的值。 |
| [!UICONTROL 分子] | `numerator` | [[!UICONTROL 数量]](../data-types/quantity.md) | 分子值。 |

>[!NOTE]
>
> 由于按照HL7 FHIR版本5创建的规范，`denominator`和`numerator`具有不同的数据类型。

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
