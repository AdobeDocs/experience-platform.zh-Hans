---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；设备；数据类型；货币；
solution: Experience Platform
title: 货币数据类型
topic-legacy: overview
description: 本文档概述了货币XDM数据类型。
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 5e92b288bb8c996cfcf343d8ac1ab1665b0d3ad0
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

#  Currencydata类型

 Currency是一种标准XDM数据类型，用于描述货币金额，包括货币类型和兑换日期。

![](../images/data-types/currency.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `amount` | 双精度 | 由`currencyCode`定义的货币金额。 |
| `conversionDate` | DateTime | 进行货币换算的时间戳。 |
| `currencyCode` | 字符串 | ISO 4217代码，用于指示`amount`表示的货币类型。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
