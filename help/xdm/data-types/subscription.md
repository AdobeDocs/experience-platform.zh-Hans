---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；订阅；数据类型；数据类型；
solution: Experience Platform
title: 订阅数据类型
description: 了解订阅体验数据模型(XDM)数据类型。
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 28%

---

# [!UICONTROL 订阅]数据类型

[!UICONTROL 订阅]是一个标准的体验数据模型(XDM)数据类型，它描述了对软件、服务或商品的许可权利，这些软件、服务或商品是根据时间或使用情况而使用的。

![](../images/data-types/subscription-data-type.png){width=500}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `device` | [[!UICONTROL 设备]](./device.md) | 描述有关链接到订阅的设备的详细信息。 |
| `environment` | [[!UICONTROL 环境]](./environment.md) | 包含有关发生事件观察的周边情况的信息，尤其会详细说明网络或软件版本等临时信息。 |
| `subscriber` | [[!UICONTROL 人员]](./person.md) | 描述个人。 这还可以表示担任各种角色的人员，例如客户、联系人或所有者。 |
| `SKU` | 字符串 | 库存单位(SKU)，产品的唯一标识符。 |
| `billingPeriod` | 字符串 | 计费间隔时间。 |
| `billingStartDate` | 日期 | 第一张账单到期的日期。 日期格式（不带时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `category` | 字符串 | 此类订阅的主要顶级分类。 |
| `chargeMethod` | 字符串 | 向客户收费的计费方式。 |
| `contractID` | 字符串 | 管理此订阅的合同的唯一ID。 |
| `country` | 字符串 | 订阅合同和协议条款所在的国家/地区。 |
| `endDate` | 日期 | 当前订阅期的结束日期。 日期格式（不带时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `paymentMethod` | 字符串 | 定期付款的付款方式。 |
| `paymentStatus` | 字符串 | 帐户的付款状态。 |
| `planName` | 字符串 | 易于用户识别的订阅名称。 |
| `reason` | 字符串 | 成员使用订阅的一般意图。 |
| `renew` | 字符串 | 议定的结束日期后的续订方式。 |
| `revision` | 字符串 | 相同名称和类别层级的订阅之间的标识。 |
| `startDate` | 日期 | 订阅开始的日期。 日期格式（不带时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `status` | 字符串 | 订阅的当前状态。 |
| `subCategory` | 字符串 | 订阅的特定子分类。 |
| `term` | 整数 | 订阅期限的数值。 |
| `termUnitOfTime` | 字符串 | 期限的时间单位。 |
| `topUp` | 字符串 | 描述在计费期间如何重新购买订阅的消费方面的商定条款。 |
| `type` | 字符串 | 权利的范围与订阅涵盖的人数有关。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
