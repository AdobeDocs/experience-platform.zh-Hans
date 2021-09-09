---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；保留；保留详细信息；
title: 保留详细信息架构字段组
description: 本文档概述了“保留详细信息”架构字段组。
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 5%

---


# [!UICONTROL 保留详] 细信息架构字段组

[!UICONTROL 预订] 详细信息类的标准架构字段 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 组，用于捕获有关预订的信息，包括长度、修改、可退还状态和房间数。

字段组提供单个对象类型字段`reservations`。 此对象中包含的属性说明如下。

![保留详细信息结构](../../images/field-groups/reservation-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `nonRefundableAmount` | [货币](../../data-types/currency.md) | 标记为不可退还的保留价格金额。 |
| `transaction` | [交易](../../data-types/transaction.md) | 描述保留的货币交易记录。 |
| `id` | 字符串 | 保留的唯一标识符。 |
| `cancellation` | 整数 | 在取消保留时会捕获此值。 |
| `confirmationNumber` | 字符串 | 预订的确认编号或标识符。 |
| `created` | 整数 | 创建保留后会捕获此值。 |
| `currencyCode` | 字符串 | 用于购买的ISO 4217货币代码。 |
| `endDate` | DateTime | 预订的结束下拉日期、回访日期或结帐日期。 |
| `length` | 整数 | 保留的总天数。 |
| `modification` | 整数 | 在修改保留时会捕获此值。 |
| `modificationDate` | DateTime | 上次修改保留的时间。 |
| `numberOfAdults` | 整数 | 与保留关联的成人数。 |
| `numberOfChildren` | 整数 | 与保留关联的子项数。 |
| `purpose` | 字符串 | 保留的目的，通常是企业或个人。 |
| `startDate` | DateTime | 预订的开始提货、叫客或签入日期。 |
| `triptype` | 字符串 | 指示预订是单程旅行、往返旅行还是多城市旅行。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## 特定于行业的保留字段组

还有其他几个标准字段组，这些字段组扩展了特定于行业的用例的[!UICONTROL 保留详细信息]架构。 有关更多详细信息，请参阅以下文档：

* [[!UICONTROL 餐饮预订]](./dining-reservation.md)
* [[!UICONTROL 航班预订]](./flight-reservation.md)
* [[!UICONTROL 住宿预订]](./lodging-reservation.md)