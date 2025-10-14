---
title: 装运数据类型
description: 了解配送体验数据模型(XDM)数据类型。
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 18%

---

# [!UICONTROL 送货]数据类型

[!UICONTROL 送货]是一种标准体验数据模型(XDM)数据类型，它提供与一个或多个产品的送货相关的详细信息。 其中包括物流细节和订购物品交付细节。


![&#x200B; [!UICONTROL Shipping]数据类型的图表。](../images/data-types/shipping.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL 配送方式] | `shippingMethod` | 字符串 | 客户选择的配送方式。 |
| [!UICONTROL 运费金额] | `shippingAmount` | 数字 | 客户必须支付的运费。 |
| [!UICONTROL 货币代码] | `currencyCode` | 字符串 | 用于为产品定价的 ISO 4217 字母货币代码。 |
| [!UICONTROL 送货目的地] | `shippingDestination` | 字符串 | 用户指定的收货目的地（例如，家庭、商店等）。 |
| [!UICONTROL 装运日期] | `shipDate` | 字符串 | 订单中的一个或多个项目发运的日期。 |
| [!UICONTROL 送货地址] | `address` | [[!UICONTROL 地址]](./address.md) | 送货地址。 |
| [!UICONTROL 跟踪号] | `trackingNumber` | 数字 | 装运承运人提供的跟踪编号。 |
| [!UICONTROL 跟踪URL] | `trackingURL` | 字符串 | 用于跟踪订单项目的装运状态的URL。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
