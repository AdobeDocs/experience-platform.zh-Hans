---
title: 退款项目数据类型
description: 了解退款项目体验数据模型(XDM)数据类型。
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---

# [!UICONTROL 退款项目]数据类型

[!UICONTROL 退款项目]是一种标准的体验数据模型(XDM)数据类型，用于捕获与订单关联的退款相关的信息。

![退款项数据类型的图表。](../images/data-types/refund-item.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL 交易ID] | `transactionID` | 字符串 | 此退款物料的唯一交易记录标识符。 |
| [!UICONTROL 退款金额] | `refundAmount` | 数字 | 退款的值。 |
| [!UICONTROL 退款原因] | `refundReason` | 字符串 | 发出退款的原因。 |
| [!UICONTROL 退款付款类型] | `refundPaymentType` | 字符串 | 此订单的付款方式。 允许使用自定义值。 |
| [!UICONTROL 货币代码] | `currencyCode` | 字符串 | 用于此退款项目的ISO 4217货币代码。 例如：“USD”、“EUR”。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
