---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地址；xdm:address；数据类型；数据类型；
solution: Experience Platform
title: 产品列表项数据类型
topic-legacy: overview
description: 本文档概述了产品列表项XDM数据类型。
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# [!UICONTROL 产品列表项] 目数据类型

[!UICONTROL 产品列] 表项是一种标准的XDM数据类型，用于描述客户选择的具有特定时间点的特定选项、定价和使用上下文的产品。

此数据类型中捕获的值可能与产品记录不同。 例如，产品记录包含产品信息系统中与所有客户一致的详细信息，其中产品清单项目具有在购买时向客户提供的实际价格，这可能因促销活动或季节性定价而异。

![](../images/data-types/product-list-item.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `SKU` | [!UICONTROL 字符串] | 库存单位(SKU)，由供应商定义的产品的唯一标识符。 |
| `_id` | [!UICONTROL 字符串] | 此产品条目的行项目标识符。 通过`product`标识产品本身。 |
| `currencyCode` | [!UICONTROL 字符串] | 用于为产品定价的[ISO 4217](https://www.iso.org/iso-4217-currency-codes.html)字母货币代码。 |
| `name` | [!UICONTROL 字符串] | 产品的显示名称，显示给此产品视图的用户。 |
| `priceTotal` | [!UICONTROL 双精度] | 产品行项目的总价格。 |
| `product` | [!UICONTROL 字符串] (URI) | 捕获产品本身的XDM架构的URI `$id`。 |
| `productAddMethod` | [!UICONTROL 字符串] | 访客用于将产品项目添加到列表的方法。 |
| `quantity` | [!UICONTROL 整数] | 客户表示他们需要产品的件数。 |

{style=&quot;table-layout:auto&quot;}

有关邮政地址数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
