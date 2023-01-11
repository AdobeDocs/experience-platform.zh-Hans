---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；订阅；数据类型；数据类型；
solution: Experience Platform
title: 订阅数据类型
description: 本文档概述了订阅体验数据模型(XDM)数据类型。
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 10%

---

# [!UICONTROL 订阅] 数据类型

[!UICONTROL 订阅] 是一种标准的Experience Data Model(XDM)数据类型，用于描述根据时间或使用情况对软件、服务或商品进行使用的授权许可。

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `device` | [[!UICONTROL 设备]](./device.md) | 描述有关链接到订阅的设备的详细信息。 |
| `environment` | [[!UICONTROL 环境]](./environment.md) | 包含有关事件观察所发生的周围情况的信息，特别是详细说明过渡信息，如网络或软件版本。 |
| `subscriber` | [[!UICONTROL 人员]](./person.md) | 描述个人。 这也可以表示以各种角色（如客户、联系人或所有者）行事的人员。 |
| `SKU` | 字符串 | 库存单位(SKU)，产品的唯一标识符。 |
| `billingPeriod` | 字符串 | 付款之间的持续时间。 |
| `billingStartDate` | 日期 | 第一张账单到期的日期。 日期格式（无时间）应遵循 [RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `category` | 字符串 | 此类订阅的主要顶级分类。 |
| `chargeMethod` | 字符串 | 计费的设置方式来向客户收费。 |
| `contractID` | 字符串 | 控制此订阅的合同的唯一ID。 |
| `country` | 字符串 | 订购合同和协议条款根植的国家/地区。 |
| `endDate` | 日期 | 当前订阅条款结束的日期。 日期格式（无时间）应遵循 [RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `paymentMethod` | 字符串 | 定期付款的付款方法。 |
| `paymentStatus` | 字符串 | 帐户的付款状态。 |
| `planName` | 字符串 | 订阅的人类可读名称。 |
| `reason` | 字符串 | 成员使用订阅的一般意图。 |
| `renew` | 字符串 | 订购可在结束日期后继续的约定方式。 |
| `revision` | 字符串 | 同名订阅和类别层次结构之间的标识。 |
| `startDate` | 日期 | 订阅开始的日期。 日期格式（无时间）应遵循 [RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `status` | 字符串 | 订阅的当前状态。 |
| `subCategory` | 字符串 | 订阅的特定子分类。 |
| `term` | 整数 | 订阅术语的数值。 |
| `termUnitOfTime` | 字符串 | 期间的时间单位。 |
| `topUp` | 字符串 | 描述有关如何在账单期间购回订阅消耗品方面的协议条款。 |
| `type` | 字符串 | 与订购涉及的人数有关的权利范围。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
