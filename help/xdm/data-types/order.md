---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；顺序；数据类型；数据类型；
solution: Experience Platform
title: 订单数据类型
description: 了解订单体验数据模型(XDM)数据类型。
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# [!UICONTROL 订单]数据类型

[!UICONTROL 订单]是描述产品列表订单的标准体验数据模型(XDM)数据类型。

![&#x200B; [!UICONTROL 订单]数据类型的图表。](../images/data-types/order.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| Purchase ID | `purchaseID` | 字符串 | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的，因为此ID由卖方定义。 |
| 采购订单号 | `purchaseOrderNumber` | 字符串 | 购买者为此购买或合同分配的唯一标识符。 |
| 付款清单 | `payments` | [[!UICONTROL 付款项]](./payment-item.md)的数组 | 此订单的付款清单。 付款在[!UICONTROL 付款项]规格中详细。 |
| 退款列表 | `refunds` | [[!UICONTROL 退款项目]](./refund-item.md)的数组 | 此订单的退款列表。 退款在[!UICONTROL 退款项目]规范中详述。 |
| 返回信息 | `returns` | [[!UICONTROL 返回信息]](./return.md) | RMA（退货授权）已签发。 在[!UICONTROL 返回信息]规范中详细介绍了返回情况。 |
| 货币 | `currencyCode` | 字符串 | 用于订单总额的ISO 4217货币代码。 示例包括`USD`和`EUR`。 所有实例必须匹配模式`^[A-Z]{3}$`。 |
| 税额 | `taxAmount` | 数值 | 买方作为最终付款的一部分所支付的税额。 |
| 折扣金额 | `discountAmount` | 数值 | 常规价格与适用于整个订单（而非单个产品）的特殊价格之间的差额。 |
| 价格总计 | `priceTotal` | 数值 | 应用所有折扣和税费后此订单的总价。 |
| 订单类型 | `orderType` | 字符串 | 已下订单的类型。 可能的值为`checkout`和`instant_purchase`。 |
| 最后更新日期 | `lastUpdatedDate` | 字符串 | 在商业系统中上次更新特定订单记录的时间。 格式：日期时间。 |
| 创建日期 | `createdDate` | 字符串 | 在商业系统中创建新订单的时间/日期。 格式：日期时间。 |
| 取消日期 | `cancelDate` | 字符串 | 购物者启动订单取消的日期/时间。 格式：日期时间。 |
| 已退还总额 | `refundTotal` | 数值 | 订单上此退款中提供的总额，组合了所有退款项目和任何折扣后等。 中所有规则都适用的URL的区域。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
