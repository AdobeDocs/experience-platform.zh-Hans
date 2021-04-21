---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；顺序；datatype；数据类型；
solution: Experience Platform
title: 订单数据类型
topic-legacy: overview
description: 本文档概述了订单体验数据模型(XDM)数据类型。
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---

# [!UICONTROL Order] 数据类型

[!UICONTROL Order] 是一个标准的体验数据模型(XDM)数据类型，用于描述为产品列表下单。

<img src="../images/data-types/order.PNG" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `payments` | [[!UICONTROL Payment Items]](./payment-item.md)的数组 | 此订单的付款列表。 |
| `currencyCode` | 字符串 | 用于订单合计的ISO 4217货币代码。 所有实例都必须符合常规表达式`^[A-Z]{3}$`。 示例包括 `USD` 和 `EUR`。 |
| `priceTotal` | 双精度 | 已应用所有折扣和税后此订单的总价。 |
| `purchaseID` | 字符串 | 由卖家为此购买或合同分配的唯一标识符。 由于这是由卖家定义的，因此无法保证该ID是唯一的。 |
| `purchaseOrderNumber` | 字符串 | 购买者为此购买或合同分配的唯一标识符。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
