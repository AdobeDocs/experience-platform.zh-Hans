---
title: 可编码的概念数据类型
description: 了解可编码概念Experience Data Model (XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# [!UICONTROL 可编码概念]数据类型

[!UICONTROL 可编码的概念]是一种标准的体验数据模型(XDM)数据类型，用于描述从一个资源到另一个资源的引用。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![可编码概念数据类型结构](../../../images/healthcare/data-types/codeable-concept.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 编码] | `coding` | [[!UICONTROL 编码]](../data-types/coding.md)的数组 | 由术语系统定义的代码。 |
| [!UICONTROL 文本] | `text` | 字符串 | 概念的纯文本表示形式。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
