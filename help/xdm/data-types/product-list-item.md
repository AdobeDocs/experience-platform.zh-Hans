---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地址；xdm:address；数据类型；数据类型；
solution: Experience Platform
title: 产品列表项数据类型
topic-legacy: overview
description: 本文档概述了产品列表项XDM数据类型。
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: 43157ed2b633561213e67f011835449d70ead4fc
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 4%

---

# [!UICONTROL 产品列表项] 数据类型

[!UICONTROL 产品列表项] 是一种标准XDM数据类型，用于描述客户选择的产品，以及特定时间点的特定选项、定价和使用情况上下文。

此数据类型中捕获的值可能与产品记录不同。 例如，产品记录包含产品信息系统中与所有客户一致的详细信息，其中产品清单项目具有在购买时向客户提供的实际价格，这可能因促销活动或季节性定价而异。

![](../images/data-types/product-list-item.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `selectedOptions` | 对象数组 | 包含为可配置产品选择的自定义选项。 每个列表项都是具有以下属性的对象：<ul><li>`attribute`:可配置属性的名称。</li><li>`value`:属性的值。</li></ul> |
| `SKU` | [!UICONTROL 字符串] | 库存单位(SKU)，由供应商定义的产品的唯一标识符。 |
| `_id` | [!UICONTROL 字符串] | 此产品条目的行项目标识符。 产品本身通过 `product`. |
| `currencyCode` | [!UICONTROL 字符串] | 的 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 用于为产品定价的字母货币代码。 |
| `discountAmount` | [!UICONTROL 双精度] | 如果产品已折扣，则表示产品的正常价格与特殊价格之间的差额。 |
| `name` | [!UICONTROL 字符串] | 产品的显示名称，显示给此产品视图的用户。 |
| `priceTotal` | [!UICONTROL 双精度] | 产品行项目的总价格。 |
| `product` | [!UICONTROL 字符串] (URI) | URI `$id` 用于捕获产品本身的XDM模式。 |
| `productAddMethod` | [!UICONTROL 字符串] | 访客用于将产品项目添加到列表的方法。 |
| `productImageUrl` | [!UICONTROL 字符串] | 产品主图像的URL。 |
| `quantity` | [!UICONTROL 整数] | 客户表示他们需要产品的件数。 |
| `unitOfMeasureCode` | [!UICONTROL 字符串] | 标准 [度量代码单位](https://ucum.org/ucum) 与 `quantity` 属性。 |

{style=&quot;table-layout:auto&quot;}

有关邮政地址数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
