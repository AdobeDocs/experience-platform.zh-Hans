---
title: 产品类
description: 本文档概述了Experience Data Model(XDM)中的产品类。
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 7%

---

# [!UICONTROL 产品] 类

在Experience Data Model(XDM)中， [!UICONTROL 产品] 类可捕获定义零售产品的最小属性集。

![](../images/classes/product.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `productListPrice` | [货币](../data-types/currency.md) | 描述产品在销售和折扣前的默认价格。 |
| `_id` | 字符串 | 记录的唯一、系统生成的字符串标识符。 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会为其提供显式值。 但是，如果您愿意，您仍可以选择提供您自己的唯一ID值。 |
| `productDescription` | 字符串 | 产品的描述。 |
| `productID` | 字符串 | 产品的唯一标识符。 |
| `productLastModifiedDate` | DateTime | 安 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 上次修改此产品以进行任何更新的时间戳。 |
| `productManufacturedDate` | DateTime | 安 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 创建此产品的时间戳。 |
| `productName` | 字符串 | 产品的名称。 |
| `productRating` | 字符串 | 产品的客户审核评级。 |

{style=&quot;table-layout:auto&quot;}

## 兼容的字段组 {#field-groups}

Adobe提供了多个与 [!UICONTROL 产品] 类。 以下是类的一些常用字段组的列表：

* [[!UICONTROL 产品目录]](../field-groups/product/product-catalog.md)
* [[!UICONTROL 产品类别]](../field-groups/product/product-category.md)
