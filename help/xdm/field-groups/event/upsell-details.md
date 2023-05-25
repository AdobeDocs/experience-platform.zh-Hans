---
title: 追加销售详细信息架构字段组
description: 本文档概述了“追加销售详细信息”架构字段组。
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---

# [!UICONTROL 追加销售详细信息] 架构字段组

[!UICONTROL 追加销售详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md) 用于捕获有关追加销售营销事件的信息，包括有关交易的详细信息以及向客户显示优惠的不同方式。

字段组提供单个对象类型字段， `upsells`. 此对象中包含的属性说明如下。

![追加销售详细信息结构](../../images/field-groups/upsell-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `upsellImpressions` | 数组 [展示次数](../../data-types/impressions.md) | 一个数组，列出客户的录制展示（数字视图或与追加销售选件的互动）。 |
| `upsellTransaction` | [交易](../../data-types/transaction.md) | 描述追加销售的货币交易记录。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
