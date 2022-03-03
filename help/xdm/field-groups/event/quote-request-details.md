---
title: 报价请求详细信息架构字段组
description: 本文档概述了“报价请求详细信息”架构字段组。
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 6%

---

# [!UICONTROL 报价请求详细信息] 架构字段组

[!UICONTROL 报价请求详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供了 `quotes` 对方架构，该架构可捕获各种类型报价（包括保险单、医疗保健、制造订单和高科技订单）的请求流程详细信息。

![](../../images/field-groups/quote-request-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `discount` | [[!UICONTROL 货币]](../../data-types/currency.md) | 向访客显示的报价的折扣金额。 |
| `premium` | [[!UICONTROL 货币]](../../data-types/currency.md) | 向访客显示的报价的溢价金额。 |
| `location` | [!UICONTROL 字符串] | 用于在访客位置附近查找零售商的邮政编码。 |
| `requestID` | [!UICONTROL 字符串] | 报价请求的唯一标识符。 |
| `selectedRetailer` | [!UICONTROL 字符串] | 为报价请求选择的零售商（如果适用）。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
