---
title: 人名数据类型
description: 了解人名体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5dd6fda4-c076-4c34-bdd9-259203b6ea73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# [!UICONTROL 人工姓名]数据类型

[!UICONTROL 人工名称]是一种标准的体验数据模型(XDM)数据类型，提供了有关人工或其他生命实体的名称的信息。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![人名数据类型结构](../../../images/healthcare/data-types/human-name.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | 名称正在使用或正在使用的时段。 |
| [!UICONTROL 系列] | `family` | 字符串 | 姓氏。 |
| [!UICONTROL 给定] | `given` | 字符串数组 | 名字，包括任何中间名。 |
| [!UICONTROL 前缀] | `prefix` | 字符串数组 | 给定名称或名字之前的任何名称部分。 |
| [!UICONTROL 后缀] | `suffix` | 字符串数组 | 姓氏或姓氏之后的任何部分。 |
| [!UICONTROL 文本] | `text` | 字符串 | 全名的纯文本表示形式。 |
| [!UICONTROL 使用] | `use` | 字符串 | 名称的使用。 此属性的值必须等于以下一个或多个已知枚举值。 <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
