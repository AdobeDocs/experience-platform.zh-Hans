---
title: 数量数据类型
description: 了解数量体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 881fe8a4-0253-4b75-9833-b97bb50cc87e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 10%

---

# [!UICONTROL 数量]数据类型

[!UICONTROL Quantity]是标准体验数据模型(XDM)数据类型，可提供测量或可衡量的数量。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![数量数据类型结构](../../../images/healthcare/data-types/quantity.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 代码] | `code` | 字符串 | 单位的编码形式。 |
| [!UICONTROL 比较器] | `comparator` | 字符串 | 比较运算符。 此属性的值必须等于以下已知枚举值之一。 <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL 系统] | `system` | 字符串 | 定义编码单位形式的系统，表示为URI。 |
| [!UICONTROL 单位] | `unit` | 字符串 | 单位表示。 |
| [!UICONTROL 值] | `value` | 两次 | 数值。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
