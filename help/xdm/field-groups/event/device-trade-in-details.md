---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；设备；贸易；贸易；
solution: Experience Platform
title: 设备交易详细信息架构字段组
topic-legacy: overview
description: 本文档概述了“设备交易详细信息”架构字段组。
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 4%

---

# [!UICONTROL 设备交易详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 设备更换详] 细信息是类的标准架构字 [[!DNL XDM ExperienceEvent] 段组](../../classes/experienceevent.md)。它提供了单个字段(`deviceTradeInDetails`)，用于描述设备内交易，包括内部交易值、原始设备ID和新设备ID。

![设备更换详细信息结构](../../images/field-groups/device-trade-in-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `tradeInValue` | [货币](../../data-types/currency.md) | 正在交易的设备的值。 |
| `newDeviceID` | 字符串 | 要交易的新设备的ID。 |
| `originalDeviceID` | 字符串 | 正在交易的设备的ID。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
