---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；ExperienceEvent；字段；架构；架构设计；字段组；字段组；设备；交易；折价购买；
solution: Experience Platform
title: 设备以旧换新详细信息架构字段组
description: 了解设备以旧换新详细信息架构字段组。
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# [!UICONTROL 设备以旧换新详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 查看文档 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL 设备以旧换新详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 它提供单个字段(`deviceTradeInDetails`)描述了设备以旧换新交易，包括折价价值、原始设备ID和新设备ID。

![设备以旧换新详细信息结构](../../images/field-groups/device-trade-in-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `tradeInValue` | [货币](../../data-types/currency.md) | 正在交易的设备的值。 |
| `newDeviceID` | 字符串 | 被交易的新设备的ID。 |
| `originalDeviceID` | 字符串 | 正在交易的设备的ID。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
