---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；预订；投放；
title: 航班预订方案字段组
description: 本文档概述了飞行预订架构字段组。
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 4%

---


# [!UICONTROL 飞行] 预留架构字段组

[!UICONTROL 飞行] 预订是类的标准架构字段组， [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 用于捕获有关飞行预订的信息。

字段组是[!UICONTROL Reservation Details]字段组的扩展，并包含单个对象类型字段`reservations`下的所有相同字段。 除了这些通用字段外，[!UICONTROL 飞行预订]还包括`flightReservations`数组。 该对象数组用于描述一个或多个具有航空旅行特有属性的预订。

>[!NOTE]
>
>本文档介绍`flightReservations`阵列的详细信息。 有关在`reservations`对象下提供的其他字段的信息，请参阅[[!UICONTROL 保留详细信息]字段组引用](./reservation-details.md)。

![飞行预订结构](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` 是表示飞行保留列表的对象数组。例如，如果预订事件涉及对一次行程中多个连接航班的预订，则这些预订可以列为单个事件的`flightReservations`下的单个对象。

下面提供了`flightReservations`下提供的每个对象的结构。

![flightReservations结构](../../images/field-groups/flight-reservation/flightReservations.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `flightCheckIn` | 对象 | 捕获有关飞行登记的详细信息。 该对象包含以下属性：<ul><li>`arrivalAirportCode`:（字符串）到达城市的机场代码。</li><li>`boardingGroup`:（字符串）特定于航空公司的登机顺序指示器。</li><li>`checkInMethod`:（字符串）使用签入的方法，例如计数器、在线、网亭或自助服务。</li><li>`checkedBags`:（整数）为飞行检查的包数。</li><li>`checkedPassengers`:（整数）为同一预订号码存在多个乘客时，登记的航班乘客数。</li><li>`confirmationNumber`:（字符串）预订确认编号或标识符。</li><li>`departureAirportCode`:（字符串）出发城市的机场代码。</li><li>`flightNumber`:（字符串）要保留的航班的航班号。</li></ul> |
| `flightStatusSearch` | 对象 | 捕获在搜索航班状态时返回的详细信息。 该对象包含以下属性：<ul><li>`arrivalAirportCode`:（字符串）到达城市的机场代码。</li><li>`boardingGroup`:（字符串）特定于航空公司的登机顺序指示器。</li><li>`departureAirportCode`:（字符串）出发城市的机场代码。</li><li>`departureDate`:(DateTime)正在预订的航班的出发日期。</li><li>`flightNumber`:（字符串）要保留的航班的航班号。</li><li>`searchCount`:（整数）搜索预留航班状态的次数。</li></ul> |
| `agentID` | 字符串 | 负责预订预订的代理或预订者（如果适用）。 |
| `aircraftID` | 字符串 | 飞机的标识符。 |
| `aircraftType` | 字符串 | 飞机的类型。 |
| `arrivalAirportCode` | 字符串 | 到达城市的机场代码。 |
| `arrivalDate` | DateTime | 预订的航班的到达日期。 |
| `cancellation` | 整数 | 在取消保留时会捕获此值。 |
| `confirmationNumber` | 字符串 | 预订确认号或标识符。 |
| `created` | 字符串 | 创建保留后会捕获此值。 |
| `currencyCode` | 字符串 | 用于购买的ISO 4217货币代码。 |
| `departureAirportCode` | 字符串 | 出发城的机场代码。 |
| `departureDate` | DateTime | 预定航班的出发日期。 |
| `fareClass` | 字符串 | 预订的航班的票价。 |
| `flightNumber` | 字符串 | 要保留的航班号。 |
| `length` | 整数 | 保留的总天数。 |
| `loyaltyID` | 字符串 | 预订中所列乘客的忠诚度或奖励计划ID。 |
| `modification` | 整数 | 在修改保留时会捕获此值。 |
| `modificationDate` | DateTime | 上次修改保留的时间。 |
| `numberOfAdults` | 整数 | 与保留关联的成人数。 |
| `numberOfChildren` | 整数 | 与保留关联的子项数。 |
| `passengerID` | 字符串 | 与预订相关联的乘客信息。 |
| `purpose` | 字符串 | 保留的目的，通常是企业或个人。 |
| `salesChannel` | 字符串 | 预订所在的销售渠道。 |
| `securityScreening` | 字符串 | 对乘客进行安全检查的类型。 |
| `status` | 字符串 | 航班预订的状态。 |
| `ticketNumber` | 字符串 | 保留编号或标识符。 |
| `tripType` | 字符串 | 指示预订是单程旅行、往返旅行还是多城市旅行。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
