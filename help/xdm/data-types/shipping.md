---
title: 装运数据类型
description: 了解配送体验数据模型(XDM)数据类型。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 6%

---

# [!UICONTROL 配送] 数据类型

[!UICONTROL 配送] 是一个标准体验数据模型(XDM)数据类型，它提供与一个或多个产品的装运相关的详细信息。 其中包括物流细节和订购物品交付细节。


![的图表 [!UICONTROL 配送] 数据类型。](../images/data-types/shipping.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL 配送方式] | `shippingMethod` | 字符串 | 客户选择的配送方式。 |
| [!UICONTROL 运费金额] | `shippingAmount` | 数字 | 客户必须支付的运费。 |
| [!UICONTROL 货币代码] | `currencyCode` | 字符串 | 用于为产品定价的ISO 4217字母货币代码。 |
| [!UICONTROL 配送目标] | `shippingDestination` | 字符串 | 用户指定的收货目的地（例如，家庭、商店等）。 |
| [!UICONTROL 装运日期] | `shipDate` | 字符串 | 订单中的一个或多个项目发运的日期。 |
| [!UICONTROL 配送地址] | `address` | [[!UICONTROL 地址]](./address.md) | 送货地址。 |
| [!UICONTROL 跟踪号] | `trackingNumber` | 数字 | 装运承运人提供的跟踪编号。 |
| [!UICONTROL 跟踪URL] | `trackingURL` | 字符串 | 用于跟踪订单项目的装运状态的URL。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
