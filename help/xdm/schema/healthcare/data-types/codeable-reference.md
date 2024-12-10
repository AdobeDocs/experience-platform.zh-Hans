---
title: 可编码引用数据类型
description: 了解Codeable Reference Experience Data Model (XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# [!UICONTROL 可编码引用]数据类型

[!UICONTROL 可编码引用]是描述对资源或概念的引用的标准体验数据模型(XDM)数据类型。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![可编码引用数据类型结构](../../../images/healthcare/data-types/codeable-reference.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 概念] | `concept` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 对概念的引用（按类）。 |
| [!UICONTROL 引用] | `reference` | [[!UICONTROL 引用]](../data-types/reference.md) | 对资源的引用。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
