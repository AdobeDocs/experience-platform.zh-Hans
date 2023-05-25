---
title: 报价请求详细信息架构字段组
description: 本文档概述了Quote Request Details架构字段组。
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# [!UICONTROL 报价请求详细信息] 架构字段组

[!UICONTROL 报价请求详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供一个 `quotes` 对象，捕获各种类型的报价（包括保单、医疗保健、制造订单和高科技订单）的请求流程详细信息。

![](../../images/field-groups/quote-request-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `discount` | [[!UICONTROL 货币]](../../data-types/currency.md) | 向访客显示的报价的折扣金额。 |
| `premium` | [[!UICONTROL 货币]](../../data-types/currency.md) | 向访客显示的报价的溢价金额。 |
| `location` | [!UICONTROL 字符串] | 用于查找访客所在位置附近的零售商的邮政编码。 |
| `requestID` | [!UICONTROL 字符串] | 报价请求的唯一标识符。 |
| `selectedRetailer` | [!UICONTROL 字符串] | 报价请求的选定零售商（如果适用）。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
