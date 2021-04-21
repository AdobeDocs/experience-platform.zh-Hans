---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;订阅；数据类型；数据类型；
solution: Experience Platform
title: 订阅数据类型
topic-legacy: overview
description: 本文档概述了订阅体验数据模型(XDM)数据类型。
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 9%

---

# [!UICONTROL Subscription] 数据类型

[!UICONTROL Subscription] 是一种标准的体验数据模型(XDM)数据类型，用于描述根据时间或使用情况对使用的软件、服务或商品的授权许可。

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `device` | [[!UICONTROL Device]](./device.md) | 描述有关链接到订阅的设备的详细信息。 |
| `environment` | [[!UICONTROL Environment]](./environment.md) | 包含有关事件观察发生的周围情况的信息，特别是详细说明网络或软件版本等暂时信息。 |
| `subscriber` | [[!UICONTROL Person]](./person.md) | 描述个人。 这也可以代表担任各种角色的人员，如客户、联系人或所有者。 |
| `SKU` | 字符串 | 库存单位(SKU)，产品的唯一标识符。 |
| `billingPeriod` | 字符串 | 付款之间的持续时间。 |
| `billingStartDate` | Date | 第一张账单到期的日期。 日期格式（无时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `category` | 字符串 | 此类型订阅的主顶级分类。 |
| `chargeMethod` | 字符串 | 设置向客户收费的方式。 |
| `contractID` | 字符串 | 约束此订阅的合同的唯一ID。 |
| `country` | 字符串 | 订阅合同和协议条款所根植的国家。 |
| `endDate` | 日期 | 当前订阅词结束的日期。 日期格式（无时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `paymentMethod` | 字符串 | 循环付款的付款方法。 |
| `paymentStatus` | 字符串 | 帐户的付款状态。 |
| `planName` | 字符串 | 订阅的可读名称。 |
| `reason` | 字符串 | 成员使用订阅的一般意图。 |
| `renew` | 字符串 | 订阅可在结束日期后继续的约定方式。 |
| `revision` | 字符串 | 同名订阅和类别层次之间的标识。 |
| `startDate` | 日期 | 订阅开始的日期。 日期格式（无时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `status` | 字符串 | 订阅的当前状态。 |
| `subCategory` | 字符串 | 订阅的特定子分类。 |
| `term` | 整数 | 订阅项的数值。 |
| `termUnitOfTime` | 字符串 | 期限期间的时间单位。 |
| `topUp` | 字符串 | 描述在账单期间如何购回订阅的耗材方面的协议条款。 |
| `type` | 字符串 | 权利范围与订阅涵盖的人数有关。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
