---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；电信；订阅；数据类型；数据类型；
solution: Experience Platform
title: 电信订阅数据类型
description: 本文档概述了电信订阅体验数据模型(XDM)数据类型。
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 10%

---

# [!UICONTROL 电信订购] 数据类型

[!UICONTROL 电信订购] 是一种标准的体验数据模型(XDM)数据类型，用于描述特定电信订阅类型（如internet、移动设备、媒体或固定电话）的详细信息。

>[!NOTE]
>
>本文档介绍数据类型。 对于同名的字段组，请参阅 [[!UICONTROL 电信订购] 字段组参考指南](../field-groups/profile/telecom-subscription.md).
>
>如果您描述的订阅类型与电信行业无关，请使用通用 [[!UICONTROL 订阅] 数据类型](./subscription.md) 中。

![电信订购结构](../images/data-types/telecom-subscription/structure.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `devices` | 对象数组 | 描述与计划关联的设备和/或附件的列表。 请参阅 [下方](#devices) 以了解每个数组项目的预期结构的详细信息。 |
| `subscriber` | [[!UICONTROL 人员]](./person.md) | 描述订阅的所有者。 |
| `ID` | 字符串 | 订阅实例的唯一标识符。 |
| `billingPeriod` | 字符串 | 付款之间的持续时间。 |
| `billingStartDate` | 日期 | 开单期开始的日期。 日期格式（无时间）应遵循 [RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `chargeMethod` | 字符串 | 计费的设置方式来向客户收费。 |
| `contractID` | 字符串 | 控制此订阅的合同的唯一ID。 |
| `country` | 字符串 | 订购合同和协议条款根植的国家/地区。 |
| `endDate` | 日期 | 当前订阅条款结束的日期。 日期格式（无时间）应遵循 [RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `paymentDueDate` | 日期 | 订阅付款到期的日期。 日期格式（无时间）应遵循 [RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `paymentMethod` | 字符串 | 定期付款的付款方法。 |
| `paymentStatus` | 字符串 | 帐户的付款状态。 |
| `planName` | 字符串 | 订阅的人类可读名称。 |
| `reason` | 字符串 | 成员使用订阅的一般意图。 |
| `renew` | 字符串 | 订购可在结束日期后继续的约定方式。 |
| `startDate` | 日期 | 订阅开始的日期。 日期格式（无时间）应遵循 [RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `status` | 字符串 | 订阅的当前状态。 |
| `subscriptionCategory` | 字符串 | 此类订阅的主要顶级分类。 |
| `subscriptionSKU` | 字符串 | 订阅的库存单位(SKU)。 |
| `subscriptionSubCategory` | 字符串 | 订阅的特定子分类。 |
| `term` | 整数 | 订阅术语的数值。 |
| `termUnitOfTime` | 字符串 | 期间的时间单位。 |
| `topUp` | 字符串 | 描述有关如何在账单期间购回订阅消耗品方面的协议条款。 |
| `type` | 字符串 | 与订购涉及的人数有关的权利范围。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` 是对象数组，每个对象描述与订阅相关联的设备或附件。

![器件阵列结构](../images/data-types/telecom-subscription/devices.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `deviceFees` | 对象 | 用于捕获路由器、调制解调器和接收器等项目的任何设备费用的对象。 需要以下属性：<ul><li>`amount`:货币金额，以 `currencyCode`.</li><li>`conversionDate`:货币兑换的日期。</li><li>`currencyCode`:的 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 货币代码 `amount`.</li></ul> |
| `ID` | 字符串 | 设备的唯一ID。 |
| `OS` | 字符串 | 设备操作系统。 |
| `deviceInsurance` | 字符串 | 指示客户是否已选择为此设备投保。 |
| `manufacturer` | 字符串 | 设备制造商。 |
| `name` | 字符串 | 设备的名称。 |
| `paymentOptions` | 字符串 | 指示设备是分期付款还是全额零售价格。 |
| `serialNumber` | 字符串 | 设备序列号。 |
| `status` | 字符串 | 设备状态。 |
| `storageCapacity` | 字符串 | 设备存储容量。 |
| `type` | 字符串 | 设备类型。 |

{style=&quot;table-layout:auto&quot;}
