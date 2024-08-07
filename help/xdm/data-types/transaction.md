---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；交易；数据类型；数据类型；
title: 交易数据类型
description: 了解Transaction Experience Data Model (XDM)数据类型。
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 7%

---

# [!UICONTROL 事务]数据类型

[!UICONTROL 交易]是描述货币交易详细信息的标准体验数据模型(XDM)数据类型。

![事务结构](../images/data-types/transaction.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL 货币]](./currency.md) | 描述作为交易的一部分交换的货币金额。 |
| `transactionDate` | [!UICONTROL 日期时间] | 事务发生时间的时间戳。 |
| `transactionId` | [!UICONTROL 字符串] | 交易的唯一标识符。 |
| `transactionType` | [!UICONTROL 字符串] | 访客使用的交易类型。 |

{style="table-layout:auto"}
