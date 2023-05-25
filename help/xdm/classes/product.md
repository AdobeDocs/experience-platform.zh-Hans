---
title: 产品类别
description: 本文档概述了Experience Data Model (XDM)中的Product类。
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 6%

---

# [!UICONTROL 产品] 类

在Experience Data Model (XDM)中， [!UICONTROL 产品] 类捕获定义零售产品的最小属性集。

![](../images/classes/product.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `productListPrice` | [货币](../data-types/currency.md) | 描述产品在销售和折扣前的默认价格。 |
| `_id` | 字符串 | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此不会在数据引入期间向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。 |
| `productDescription` | 字符串 | 产品的描述。 |
| `productID` | 字符串 | 产品的唯一标识符。 |
| `productLastModifiedDate` | 日期时间 | An [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 上次修改此产品以进行任何更新的时间戳。 |
| `productManufacturedDate` | 日期时间 | An [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 创建此产品的时间戳。 |
| `productName` | 字符串 | 产品的名称。 |
| `productRating` | 字符串 | 产品的客户评论评级。 |

{style="table-layout:auto"}

## 兼容的字段组 {#field-groups}

Adobe提供了多个标准字段组以用于 [!UICONTROL 产品] 类。 以下是类的一些常用字段组的列表：

* [[!UICONTROL 产品目录]](../field-groups/product/product-catalog.md)
* [[!UICONTROL 产品类别]](../field-groups/product/product-category.md)
