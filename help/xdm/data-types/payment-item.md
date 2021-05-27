---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；付款项；数据类型；数据类型；
solution: Experience Platform
title: 付款项数据类型
topic-legacy: overview
description: 本文档概述了付款项目体验数据模型(XDM)数据类型。
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---

# [!UICONTROL 付款项] 数据类型

[!UICONTROL 付款] 项是标准的体验数据模型(XDM)数据类型，用于描述与订单关联的付款，订单定义付款类型、金额和关联币种。

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `currencyCode` | 字符串 | 用于订单合计的ISO 4217货币代码。 所有实例都必须符合正则表达式`^[A-Z]{3}$`。 示例包括 `USD` 和 `EUR`。 |
| `paymentAmount` | 双精度 | 付款的值。 |
| `paymentType` | 字符串 | 此订单的付款方式。 接受的枚举值包括： <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 字符串 | 此付款项的唯一标识符。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
