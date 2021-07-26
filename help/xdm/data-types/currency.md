---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；设备；数据类型；货币；
solution: Experience Platform
title: 货币数据类型
topic-legacy: overview
description: 本文档概述了货币XDM数据类型。
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 5%

---

#  Currencydata类型

 Currency是一种标准XDM数据类型，用于描述货币金额，包括货币类型和兑换日期。

![](../images/data-types/currency.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `amount` | 双精度 | 显示可表示的颜色数。 |
| `conversionDate` | DateTime | 显示可表示的颜色数。 |
| `currencyCode` | 字符串 | 显示可表示的颜色数。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)