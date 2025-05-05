---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；电信；订阅；数据类型；数据类型；
solution: Experience Platform
title: 电信订阅数据类型
description: 了解电信订阅体验数据模型(XDM)数据类型。
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 20%

---

# [!UICONTROL 电信订阅]数据类型

[!UICONTROL 电信订阅]是标准体验数据模型(XDM)数据类型，用于描述特定电信订阅类型（如互联网、移动设备、媒体或固定电话）的详细信息。

>[!NOTE]
>
>本文档介绍了数据类型。 对于同名的字段组，请参阅[[!UICONTROL 电信订阅]字段组参考指南](../field-groups/profile/telecom-subscription.md)。
>
>如果您描述的订阅类型与电信行业无关，请改用通用[[!UICONTROL 订阅]数据类型](./subscription.md)。

![电信订阅结构](../images/data-types/telecom-subscription/structure.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `devices` | 对象数组 | 描述与计划关联的设备和/或附件的列表。 有关每个数组项的预期结构的详细信息，请参阅下面[&#128279;](#devices)的部分。 |
| `subscriber` | [[!UICONTROL 人员]](./person.md) | 描述订阅的所有者。 |
| `ID` | 字符串 | 订阅实例的唯一标识符。 |
| `billingPeriod` | 字符串 | 计费间隔时间。 |
| `billingStartDate` | 日期 | 计费期间开始的日期。 日期格式（不带时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `chargeMethod` | 字符串 | 向客户收费的计费方式。 |
| `contractID` | 字符串 | 管理此订阅的合同的唯一ID。 |
| `country` | 字符串 | 订阅合同和协议条款所在的国家/地区。 |
| `endDate` | 日期 | 当前订阅期的结束日期。 日期格式（不带时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `paymentDueDate` | 日期 | 订阅付款到期的日期。 日期格式（不带时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `paymentMethod` | 字符串 | 定期付款的付款方式。 |
| `paymentStatus` | 字符串 | 帐户的付款状态。 |
| `planName` | 字符串 | 易于用户识别的订阅名称。 |
| `reason` | 字符串 | 成员使用订阅的一般意图。 |
| `renew` | 字符串 | 议定的结束日期后的续订方式。 |
| `startDate` | 日期 | 订阅开始的日期。 日期格式（不带时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `status` | 字符串 | 订阅的当前状态。 |
| `subscriptionCategory` | 字符串 | 此类订阅的主要顶级分类。 |
| `subscriptionSKU` | 字符串 | 订阅的库存单位(SKU)。 |
| `subscriptionSubCategory` | 字符串 | 订阅的特定子分类。 |
| `term` | 整数 | 订阅期限的数值。 |
| `termUnitOfTime` | 字符串 | 期限的时间单位。 |
| `topUp` | 字符串 | 描述在计费期间如何重新购买订阅的消费方面的商定条款。 |
| `type` | 字符串 | 权利的范围与订阅涵盖的人数有关。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices`是一个对象数组，每个对象都描述与订阅关联的设备或附件。

![设备阵列结构](../images/data-types/telecom-subscription/devices.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `deviceFees` | 对象 | 捕获路由器、调制解调器和接收器等项目的任何设备费用的对象。 需要以下属性：<ul><li>`amount`： `currencyCode`表示的货币金额。</li><li>`conversionDate`：进行货币转换的日期。</li><li>`currencyCode`： `amount`的[ISO 4217](https://www.iso.org/iso-4217-currency-codes.html)货币代码。</li></ul> |
| `ID` | 字符串 | 设备的唯一ID。 |
| `OS` | 字符串 | 设备操作系统。 |
| `deviceInsurance` | 字符串 | 指示客户是否已选择为此设备投保。 |
| `manufacturer` | 字符串 | 设备制造商。 |
| `name` | 字符串 | 设备的名称。 |
| `paymentOptions` | 字符串 | 指示是分期付款还是按全额零售价支付设备。 |
| `serialNumber` | 字符串 | 设备序列号。 |
| `status` | 字符串 | 设备状态。 |
| `storageCapacity` | 字符串 | 设备存储容量。 |
| `type` | 字符串 | 设备类型。 |

{style="table-layout:auto"}
