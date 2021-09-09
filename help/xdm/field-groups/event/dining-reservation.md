---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；预订；用餐；
title: 用餐预订架构字段组
description: 本文档概述了“餐饮预订”架构字段组。
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---


# [!UICONTROL Dining Reservationschema] 字段组

[!UICONTROL Dining Reservation是] 类的标准架构字段组，用 [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 于捕获有关用餐预订的信息。

字段组是[!UICONTROL Reservation Details]字段组的扩展，并包含单个对象类型字段`reservations`下的所有相同字段。 除了这些通用字段外，[!UICONTROL Dining Reservation]还包含`diningReservations`数组。 此对象数组用于描述一个或多个具有餐厅特定属性的预订。

>[!NOTE]
>
>本文档介绍`diningReservations`阵列的详细信息。 有关在`reservations`对象下提供的其他字段的信息，请参阅[[!UICONTROL 保留详细信息]字段组引用](./reservation-details.md)。

![餐饮预订结构](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` 是表示餐饮预订列表的对象数组。例如，如果预订事件涉及在一天中不同时间在多个不同餐馆预订，则这些预订可以列为单个事件`diningReservations`下的单个对象。

下面提供了`diningReservations`下提供的每个对象的结构。

![diningReservations结构](../../images/field-groups/dining-reservation/diningReservations.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `ID` | 字符串 | 保留编号或标识符。 |
| `cancellation` | 整数 | 在取消保留时会捕获此值。 |
| `confirmationNumber` | 字符串 | 预订确认号或标识符。 |
| `created` | 整数 | 创建保留后会捕获此值。 |
| `cuisine` | 整数 | 餐厅菜的种类。 |
| `currencyCode` | 字符串 | 用于购买的ISO 4217货币代码。 |
| `deliveryPartners` | 字符串 | 餐厅提供送货合作伙伴。 |
| `diningOptions` | 字符串 | 餐厅提供送货和餐饮服务。 |
| `groupReservation` | 布尔型 | 指示是否正在为组进行保留。 |
| `length` | 整数 | 保留的总天数。 |
| `loyaltyID` | 字符串 | 预订中列出的来宾的忠诚度计划ID。 |
| `modification` | 整数 | 在修改保留时会捕获此值。 |
| `modificationDate` | DateTime | 上次修改保留的时间。 |
| `numberOfAdults` | 整数 | 与保留关联的成人数。 |
| `numberOfChildren` | 整数 | 与保留关联的子项数。 |
| `numberOfRooms` | 整数 | 与预订关联的房间数。 |
| `partySize` | 整数 | 用餐聚会上的个人数。 |
| `priceCategory` | 字符串 | 所保留的价格类别。 |
| `purpose` | 字符串 | 保留的目的，通常是企业或个人。 |
| `reservationTime` | DateTime | 预订餐饮预订的时间。 |
| `restaurantID` | 字符串 | 餐厅或餐饮场所的标识符。 |
| `reservationStatus` | 字符串 | 保留的状态。 |
| `specialOccasion` | 布尔型 | 指示是否为特殊场合提出保留。 |
| `status` | 整数 | 餐饮预订的状态。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
