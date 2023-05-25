---
title: 升级详细信息架构字段组
description: 本文档概述了“升级详细信息”架构字段组。
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---

# [!UICONTROL 升级详细信息] 架构字段组

[!UICONTROL 升级详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md) 用于捕获有关升级营销事件的信息，包括有关交易以及向客户显示优惠的不同方式的详细信息。

字段组提供单个对象类型字段， `upgrades`. 此对象中包含的属性说明如下。

![升级详细信息结构](../../images/field-groups/upgrade-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `upgradeImpressions` | 数组 [展示次数](../../data-types/impressions.md) | 一个阵列，列出客户的录制展示（数字视图或升级选件的参与）。 |
| `upgradeTransaction` | [交易](../../data-types/transaction.md) | 描述升级的货币交易记录。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
