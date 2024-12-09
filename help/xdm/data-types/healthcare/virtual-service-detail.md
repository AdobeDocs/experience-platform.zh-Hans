---
title: 虚拟服务详细信息数据类型
description: 了解虚拟服务详细信息体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# [!UICONTROL 虚拟服务详细信息]数据类型

[!UICONTROL 虚拟服务详细信息]是描述虚拟服务联系详细信息的标准体验数据模型(XDM)数据类型。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![虚拟服务详细信息数据类型结构](../../images/data-types/healthcare/virtual-service-detail.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 地址联系点] | `addressContactPoint` | [[!UICONTROL 联系点]](../healthcare/contact-point.md) | 技术媒介的联系点的详细信息，如电话、传真或电子邮件。 |
| [!UICONTROL 地址扩展联系人详细信息] | `addressExtendedContactDetail` | [[!UICONTROL 扩展的联系人详细信息]](../healthcare/extended-contact-detail.md) | 扩展的联系信息。 |
| [!UICONTROL 渠道类型] | `channelType` | [[!UICONTROL 编码]](../healthcare/coding.md) | 要连接的虚拟服务的类型，如Teams、Zoom或WhatsApp。 |
| [!UICONTROL 其他信息] | `additionalInfo` | 字符串数组 | 用于查看替代连接详细信息的地址，表示为URI。 |
| [!UICONTROL 地址字符串] | `addressString` | 字符串 | 用于连接到虚拟服务的地址。 |
| [!UICONTROL 地址Url] | `addressUrl` | 字符串 | 用于连接到虚拟服务的URL，以URI表示。 |
| [!UICONTROL 最大参与者数] | `maxParticipants` | 整数 | 支持的最大参与者数，最小值为`0`。 |
| [!UICONTROL 会话密钥] | `sessionKey` | 字符串 | 虚拟服务所需的会话密钥。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
