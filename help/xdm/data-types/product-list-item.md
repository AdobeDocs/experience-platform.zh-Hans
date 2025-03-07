---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地址；xdm：地址；数据类型；数据类型；
solution: Experience Platform
title: 产品列表项数据类型
description: 了解产品列表项XDM数据类型。
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: ba6c6eb2c6b0fc1dfc4e7440fd16a85bc7b46457
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 20%

---

# [!UICONTROL 产品列表项]数据类型

[!UICONTROL 产品列表项]是一个标准XDM数据类型，它描述了客户选择的具有特定选项、定价和使用上下文的产品。

在此数据类型中捕获的值可能与产品记录不同。 例如，产品记录包含来自产品信息系统的对所有客户一致的详细信息，其中产品列表项目具有在购买时提供给客户的实际价格，该价格可能因销售活动或季节性定价而有所不同。

![](../images/data-types/product-list-item.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `selectedOptions` | 对象数组 | 包含为可配置产品选择的自定义选项。 每个列表项都是一个具有以下属性的对象：<ul><li>`attribute`：可配置属性的名称。</li><li>`value`：属性的值。</li></ul> |
| `SKU` | [!UICONTROL 字符串] | 库存单位 (SKU)，供应商定义的产品的唯一标识符。 |
| `_id` | [!UICONTROL 字符串] | 此产品条目的行项目标识符。 通过`product`标识产品本身。 |
| `currencyCode` | [!UICONTROL 字符串] | 用于为产品定价的[ISO 4217](https://www.iso.org/iso-4217-currency-codes.html)字母货币代码。 |
| `discountAmount` | [!UICONTROL 双精度] | 如果产品打折，则表示产品正常价格与特价之间的差额。 |
| `name` | [!UICONTROL 字符串] | 在此产品视图中向用户显示的产品显示名称。 |
| `priceTotal` | [!UICONTROL 双精度] | 产品系列项目的总价。 |
| `product` | [!UICONTROL 字符串] (URI) | 产品本身的 XDM 标识符。 |
| `productAddMethod` | [!UICONTROL 字符串] | 访客用来将产品项目添加到列表的方法。 |
| `productImageUrl` | [!UICONTROL 字符串] | 产品主图像的URL。 |
| `quantity` | [!UICONTROL 整数] | 客户表明的所需产品的单位数。 |
| `unitOfMeasureCode` | [!UICONTROL 字符串] | 与`quantity`属性相关的产品的标准[度量单位代码](https://ucum.org/ucum)。 |

{style="table-layout:auto"}

有关邮政地址数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
