---
title: 升级详细信息架构字段组
description: 了解升级详细信息架构字段组。
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL 升级详细信息]架构字段组

[!UICONTROL 升级详细信息]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组，用于捕获有关升级营销事件的信息，包括有关交易以及向客户显示优惠的不同方式的详细信息。

字段组提供单个对象类型字段`upgrades`。 此对象中包含的属性说明如下。

![升级详细信息结构](../../images/field-groups/upgrade-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `upgradeImpressions` | [展示次数数组](../../data-types/impressions.md) | 一个数组，列出了客户录制的展示（数字视图或与升级选件的互动）。 |
| `upgradeTransaction` | [事务](../../data-types/transaction.md) | 描述升级的货币交易记录。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
