---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；事务；数据类型；数据类型；
title: 交易数据类型
description: 本文档概述了交易体验数据模型(XDM)数据类型。
source-git-commit: bbe5456ddba1db9044b8a7f94a7ba8e450f89f0f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 8%

---

#  Transactiondata类型

 Transaction是一种标准的体验数据模型(XDM)数据类型，用于描述货币交易的详细信息。

![交易结构](../images/data-types/transaction.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL 货币]](./currency.md) | 描述作为交易记录一部分的交换货币金额。 |
| `transactionDate` | [!UICONTROL DateTime] | 事务发生时间的时间戳。 |
| `transactionId` | [!UICONTROL 字符串] | 交易的唯一标识符。 |
| `transactionType` | [!UICONTROL 字符串] | 访客使用的交易类型。 |

{style=&quot;table-layout:auto&quot;}
