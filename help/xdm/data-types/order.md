---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；顺序；数据类型；数据类型；
solution: Experience Platform
title: 订单数据类型
description: 本文档概述了订单体验数据模型(XDM)数据类型。
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 6%

---

# [!UICONTROL 订购] 数据类型

[!UICONTROL 订购] 是一种标准的体验数据模型(XDM)数据类型，用于描述产品列表的订单。

<img src="../images/data-types/order.PNG" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `payments` | 数组 [[!UICONTROL 付款项]](./payment-item.md) | 此订单的付款清单。 |
| `currencyCode` | 字符串 | 用于订单合计的ISO 4217货币代码。 所有实例都必须符合正则表达式 `^[A-Z]{3}$`. 示例包括 `USD` 和 `EUR`。 |
| `priceTotal` | 双精度 | 在应用所有折扣和税后，此订单的总价。 |
| `purchaseID` | 字符串 | 卖方为此采购或合同分配的唯一标识符。 由于这是由卖家定义的，因此无法保证ID是唯一的。 |
| `purchaseOrderNumber` | 字符串 | 购买者为此购买或合同分配的唯一标识符。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
