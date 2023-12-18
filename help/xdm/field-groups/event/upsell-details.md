---
title: 追加销售详细信息架构字段组
description: 了解追加销售详细信息架构字段组。
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL 追加销售详细信息] 架构字段组

[!UICONTROL 追加销售详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md) 用于捕获有关追加销售营销事件的信息，包括有关交易以及向客户显示优惠的不同方式的详细信息。

字段组提供单个对象类型字段， `upsells`. 此对象中包含的属性说明如下。

![追加销售详细信息结构](../../images/field-groups/upsell-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `upsellImpressions` | 数组 [展示次数](../../data-types/impressions.md) | 一个数组，列出了客户录制的印象（数字视图或与追加销售选件的互动）。 |
| `upsellTransaction` | [交易](../../data-types/transaction.md) | 描述追加销售的货币交易记录。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
