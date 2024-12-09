---
title: 注释数据类型
description: 了解注释体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# [!UICONTROL 批注]数据类型

[!UICONTROL 批注]是标准体验数据模型(XDM)数据类型，其中包含归因于作者的文本节点。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![注释数据类型结构](../../images/data-types/healthcare/annotation.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 作者引用] | `authorReference` | [[!UICONTROL 引用]](../healthcare/reference.md) | 对作者的引用。 |
| [!UICONTROL 作者] | `authorString` | 字符串 | 负责注释的个人。 |
| [!UICONTROL 文本] | `text` | 字符串 | 注释的内容。 |
| [!UICONTROL 时间] | `time` | 日期时间 | 创建注释的时间。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
