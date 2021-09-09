---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；预订；住宿；
title: 寄宿保留方案字段组
description: 本文档概述了“住宿预订”架构字段组。
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 5%

---


# [!UICONTROL Lodging ] Reservationschema字段组

[!UICONTROL Lodging Reservation] 是类的标准架构字段组， [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 用于捕获有关Lodging Reservation的信息。

字段组是[!UICONTROL Reservation Details]字段组的扩展，并包含单个对象类型字段`reservations`下的所有相同字段。 除了这些通用字段外，[!UICONTROL Lodging Reservation]还包含`lodgingReservations`数组。 此对象数组用于描述一个或多个保留，该保留具有对于Lodging而言是唯一的属性。

>[!NOTE]
>
>本文档介绍`lodgingReservations`阵列的详细信息。 有关在`reservations`对象下提供的其他字段的信息，请参阅[[!UICONTROL 保留详细信息]字段组引用](./reservation-details.md)。

![住宿预订结构](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` 是表示住宿预订列表的对象数组。例如，如果预订事件涉及沿行程路线在多家不同酒店的预订，则这些预订可以列为单个事件的`lodgingReservations`下的单个对象。

下面提供了`lodgingReservations`下提供的每个对象的结构。

![lodgingReservations结构](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL 货币]](../../data-types/currency.md) | 旅馆房间的平均日价。 |
| `lodgingCheckIn` | 对象 | 描述提交签入详细信息的对象。 包括以下值：<ul><li>`digitalKey`:（整数）指示来宾在签入时选择使用数字键的时间。</li><li>`earlyCheckInRequested`:（整数）指示来宾请求在正常签入小时之前签入的时间。</li><li>`lateCheckInRequested`:（整数）指示来宾请求在正常签入小时之后签入的时间。</li><li>`noRoomCheckIn`:（整数）当来宾在当时没有可用的房间时完成签入时，将捕获此值。</li><li>`oneRoomCheckIn`:（整数）当来宾完成签入时，当时只有一个可用房间时，会捕获此值。</li><li>`roomKeys`:（整数）签入时提供的标准房间键数。</li><li>`userSelectedRoom`:（布尔值）指示来宾是否在签入时选择了其房间。</li></ul> |
| `rackrate` | [[!UICONTROL 货币]](../../data-types/currency.md) | 当天预订的成本，无需事先预订。 |
| `ID` | 字符串 | 保留编号或标识符。 |
| `agentID` | 字符串 | 与酒店预订关联的代理ID。 |
| `basePrice` | 字符串 | 在添加任何折扣前的基价。 |
| `bookingID` | 字符串 | 与酒店预订关联的预订ID。 |
| `cancellation` | 整数 | 在取消保留时会捕获此值。 |
| `checkInDate` | DateTime | 房间预订的登记日期。 |
| `checkOutDate` | DateTime | 房间预订的结帐日期。 |
| `confirmationNumber` | 字符串 | 预订确认号或标识符。 |
| `couponCode` | 字符串 | 与酒店预订关联的优惠券代码。 |
| `created` | 整数 | 创建保留后会捕获此值。 |
| `currencyCode` | 字符串 | 用于购买的ISO 4217货币代码。 |
| `discountPercent` | 双精度 | 与预订关联的折扣百分比。 |
| `freeCancelation` | 布尔型 | 指示文件室是否具有免费取消策略。 |
| `guestID` | 字符串 | 与酒店预订关联的来宾ID。 |
| `length` | 整数 | 保留的总天数。 |
| `loyaltyID` | 字符串 | 预订中列出的来宾的忠诚度计划ID。 |
| `modification` | 整数 | 在修改保留时会捕获此值。 |
| `modificationDate` | DateTime | 上次修改保留的时间。 |
| `numberOfAdults` | 整数 | 与保留关联的成人数。 |
| `numberOfChildren` | 整数 | 与保留关联的子项数。 |
| `numberOfRooms` | 整数 | 与预订关联的房间数。 |
| `propertyID` | 字符串 | 预订酒店或度假村的标识符。 |
| `propertyName` | 字符串 | 预订的酒店或度假村的名称。 |
| `purpose` | 字符串 | 保留的目的，通常是企业或个人。 |
| `ratePlan` | 字符串 | 房间卖的费率协议。 |
| `refundable` | 布尔型 | 指示文件室是否可退款。 |
| `reservationStatus` | 字符串 | 保留的状态。 |
| `roomAccessibilityType` | 字符串 | 房间的辅助功能类型，如移动、听力或其他。 |
| `roomCapacity` | 整数 | 酒店房间的住客人数。 |
| `roomType` | 字符串 | 要保留的房间类型。 |
| `smoking` | 布尔型 | 指示房间是否允许吸烟。 |
| `tripType` | 字符串 | 指示预订是单程旅行、往返旅行还是多城市旅行。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
