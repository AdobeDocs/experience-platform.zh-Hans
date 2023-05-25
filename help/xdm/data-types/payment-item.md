---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；付款项；数据类型；数据类型；
solution: Experience Platform
title: 付款项目数据类型
description: 本文档概述了付款项目体验数据模型(XDM)数据类型。
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 5%

---

# [!UICONTROL 付款项目] 数据类型

[!UICONTROL 付款项目] 是一个标准体验数据模型(XDM)数据类型，它描述了与订单关联的付款，定义了付款类型、金额和相关联的货币。

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `currencyCode` | 字符串 | 用于订单总额的ISO 4217货币代码。 所有实例都必须符合正则表达式 `^[A-Z]{3}$`. 示例包括 `USD` 和 `EUR`。 |
| `paymentAmount` | 双精度 | 付款的值。 |
| `paymentType` | 字符串 | 此订单的付款方式。 接受的枚举值包括： <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 字符串 | 此付款项目的唯一交易标识符。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
