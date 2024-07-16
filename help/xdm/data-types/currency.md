---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；设备；数据类型；数据类型；货币；
solution: Experience Platform
title: 货币数据类型
description: 了解货币XDM数据类型。
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 6%

---

# [!UICONTROL 货币]数据类型

[!UICONTROL Currency]是描述货币金额的标准XDM数据类型，包括货币类型和兑换日期。

![](../images/data-types/currency.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `amount` | 两次 | 由`currencyCode`定义的货币金额。 |
| `conversionDate` | 日期时间 | 进行货币转换的时间戳。 |
| `currencyCode` | 字符串 | 指示`amount`表示的货币类型的ISO 4217代码。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
