---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；预订；航班；
title: 航班预订架构字段组
description: 了解航班预订模式字段组。
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 4%

---

# [!UICONTROL 航班预订] 架构字段组

[!UICONTROL 航班预订] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md) 用于捕获有关航班预订的信息。

字段组是 [!UICONTROL 预订详细信息] 字段组，并在单个对象类型字段下包含所有相同的字段， `reservations`. 除了这些通用字段之外， [!UICONTROL 航班预订] 还包括 `flightReservations` 数组。 此对象数组用于描述一个或多个具有航空旅行特有属性的预订。

>[!NOTE]
>
>本文档介绍 `flightReservations` 数组。 有关 `reservations` 对象，请参阅 [[!UICONTROL 预订详细信息] 字段组引用](./reservation-details.md).

![航班预订结构](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` 是一个对象数组，表示航班预订列表。 例如，如果预订事件涉及为一次行程中的多个连接航班进行预订，则这些预订可作为 `flightReservations` 就为了一个事件。

下面提供的每个对象的结构 `flightReservations` 具体内容如下。

![flightReservations结构](../../images/field-groups/flight-reservation/flightReservations.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `flightCheckIn` | 对象 | 捕获有关航班登记的详细信息。 该对象包含以下属性：<ul><li>`arrivalAirportCode`：（字符串）到达城市的机场代码。</li><li>`boardingGroup`：（字符串）航空公司特定的登机订单指示器。</li><li>`checkInMethod`：（字符串）使用登记入住的方法，例如柜台、在线、自助服务亭或自助服务。</li><li>`checkedBags`：（整数）航班托运的行李数。</li><li>`checkedPassengers`：（整数）如果同一预订号存在多名乘客，则为航班办理登机手续的乘客数。</li><li>`confirmationNumber`：（字符串）预订确认编号或标识符。</li><li>`departureAirportCode`：（字符串）出发城市的机场代码。</li><li>`flightNumber`：（字符串）所预订航班的航班号。</li></ul> |
| `flightStatusSearch` | 对象 | 捕获搜索航班状态时返回的详细信息。 该对象包含以下属性：<ul><li>`arrivalAirportCode`：（字符串）到达城市的机场代码。</li><li>`boardingGroup`：（字符串）航空公司特定的登机订单指示器。</li><li>`departureAirportCode`：（字符串）出发城市的机场代码。</li><li>`departureDate`：（日期时间）所预订航班的出发日期。</li><li>`flightNumber`：（字符串）所预订航班的航班号。</li><li>`searchCount`：（整数）已搜索预订航班状态的次数。</li></ul> |
| `agentID` | 字符串 | 负责预订的代理或预订者（如果适用）。 |
| `aircraftID` | 字符串 | 飞机的标识符。 |
| `aircraftType` | 字符串 | 飞机的类型。 |
| `arrivalAirportCode` | 字符串 | 到达城市的机场代码。 |
| `arrivalDate` | 日期时间 | 所预订航班的到达日期。 |
| `cancellation` | 整数 | 此值在取消预订后捕获。 |
| `confirmationNumber` | 字符串 | 预订确认号或标识符。 |
| `created` | 字符串 | 此值在创建预订后捕获。 |
| `currencyCode` | 字符串 | 用于进行购买的ISO 4217货币代码。 |
| `departureAirportCode` | 字符串 | 出发城市的机场代码。 |
| `departureDate` | 日期时间 | 所预订航班的出发日期。 |
| `fareClass` | 字符串 | 所预订航班的票价等级。 |
| `flightNumber` | 字符串 | 所预订航班的航班号。 |
| `length` | 整数 | 预订的总天数。 |
| `loyaltyID` | 字符串 | 预订中列出的乘客的忠诚度或奖励计划ID。 |
| `modification` | 整数 | 此值在修改预订后捕获。 |
| `modificationDate` | 日期时间 | 上次修改预订的时间。 |
| `numberOfAdults` | 整数 | 与预订关联的成人数量。 |
| `numberOfChildren` | 整数 | 与预订关联的子项数。 |
| `passengerID` | 字符串 | 与预订关联的乘客信息。 |
| `purpose` | 字符串 | 预订的目的，通常是商业目的或个人目的。 |
| `salesChannel` | 字符串 | 从中预订预订的销售渠道。 |
| `securityScreening` | 字符串 | 乘客需接受的安全检查的类型。 |
| `status` | 字符串 | 航班预订的状态。 |
| `ticketNumber` | 字符串 | 预订编号或标识符。 |
| `tripType` | 字符串 | 指示预订是单程旅行、往返还是多城市旅行。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
