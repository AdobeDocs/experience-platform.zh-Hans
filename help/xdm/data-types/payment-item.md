---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；支付项目；数据类型；数据类型；
solution: Experience Platform
title: 付款项目数据类型
description: 了解支付项体验数据模型(XDM)数据类型。
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 7%

---

# [!UICONTROL 付款项目] 数据类型

[!UICONTROL 付款项目] 是一个标准的体验数据模型(XDM)数据类型，它描述了与订单关联的付款，从而定义了付款类型、金额和相关联的货币。

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
