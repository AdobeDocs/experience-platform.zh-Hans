---
title: 扩展的联系人详细信息数据类型
description: 了解扩展的联系详细信息体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 4ac9b3d7-acc8-4a82-b34f-ec63a8bf12e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 6%

---

# [!UICONTROL 扩展的联系人详细信息]数据类型

[!UICONTROL 扩展联系人详细信息]是描述扩展联系人信息的标准体验数据模型(XDM)数据类型。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![扩展的联系人详细信息数据类型结构](../../../images/healthcare/data-types/extended-contact-detail.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 地址] | `address` | [[!UICONTROL 地址]](../data-types/address.md) | 联系人的地址。 |
| [!UICONTROL 名称] | `name` | [[!UICONTROL 人工名称]](../data-types/human-name.md)的数组 | 要联系的个人的名称。 |
| [!UICONTROL 组织] | `organization` | [[!UICONTROL 引用]](../data-types/reference.md) | 处理/监控联系人详细信息的组织。 |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | 联系人的有效使用期限。 |
| [!UICONTROL 用途] | `purpose` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 联系类型。 |
| [!UICONTROL 电信] | `telecom` | [[!UICONTROL 联系点]](../data-types/contact-point.md)的数组 | 联系人详细信息。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
