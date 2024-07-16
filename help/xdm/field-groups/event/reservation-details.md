---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；保留；保留详细信息；
title: 预订详细信息架构字段组
description: 了解预订详细信息架构字段组。
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 6%

---

# [!UICONTROL 保留详细信息]架构字段组

[!UICONTROL 预订详细信息]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组，用于捕获有关预订的信息，包括时长、修改、可退款状态和房间数。

字段组提供单个对象类型字段`reservations`。 此对象中包含的属性说明如下。

![预订详细信息结构](../../images/field-groups/reservation-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `nonRefundableAmount` | [货币](../../data-types/currency.md) | 标记为不可退款的预订价格的金额。 |
| `transaction` | [事务](../../data-types/transaction.md) | 描述预订的货币交易记录。 |
| `id` | 字符串 | 预订的唯一标识符。 |
| `cancellation` | 整数 | 此值在取消预订后捕获。 |
| `confirmationNumber` | 字符串 | 预订的确认号或标识符。 |
| `created` | 整数 | 此值在创建预订后捕获。 |
| `currencyCode` | 字符串 | 用于进行购买的ISO 4217货币代码。 |
| `endDate` | 日期时间 | 预订的交车、还车或结账结束日期。 |
| `length` | 整数 | 预订的总天数。 |
| `modification` | 整数 | 此值在修改预订后捕获。 |
| `modificationDate` | 日期时间 | 上次修改预订的时间。 |
| `numberOfAdults` | 整数 | 与预订关联的成人数量。 |
| `numberOfChildren` | 整数 | 与预订关联的子项数。 |
| `purpose` | 字符串 | 预订的目的，通常是商业目的或个人目的。 |
| `startDate` | 日期时间 | 预订的开始接送、出站或登记日期。 |
| `triptype` | 字符串 | 指示预订是单程旅行、往返还是多城市旅行。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## 行业特定的预订字段组

还有其他几个标准字段组针对特定行业用例扩展了[!UICONTROL 保留详细信息]架构。 有关更多详细信息，请参阅以下文档：

* [[!UICONTROL 餐饮预订]](./dining-reservation.md)
* [[!UICONTROL 航班预订]](./flight-reservation.md)
* [[!UICONTROL 住宿预订]](./lodging-reservation.md)
