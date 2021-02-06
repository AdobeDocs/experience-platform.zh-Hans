---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；商务；数据类型；数据类型；
solution: Experience Platform
title: 商务数据类型
topic: overview
description: 此文档概述了商务体验数据模型(XDM)数据类型。
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# [!UICONTROL Commercedata] 类型

[!UICONTROL Commerce是] 一种标准的体验数据模型(XDM)数据类型，用于描述与购买和销售活动相关的记录。

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `order` | [[!UICONTROL 订单]](./order.md) | 描述一个或多个产品的下单。 |
| `cartAbandons` | [[!UICONTROL 度量]](./measure.md) | 用于描述何时产品列表被标识为用户不再可访问或可购买。 |
| `checkouts` | [[!UICONTROL 度量]](./measure.md) | 在产品列表的结帐过程中执行的操作。 如果一个结帐过程中有多个步骤，则可能存在多个结帐事件。 如果有多个步骤，则事件时间信息和引用的页面或体验用于标识步骤和按顺序表示的单个事件。 |
| `inStorePurchase` | [[!UICONTROL 度量]](./measure.md) | 描述与店内购买相关的值，供分析使用。 |
| `productListAdds` | [[!UICONTROL 度量]](./measure.md) | 将产品添加到产品列表，如添加到购物车的产品。 |
| `productListOpens` | [[!UICONTROL 度量]](./measure.md) | 新产品列表的初始化，如正在创建的购物车。 |
| `productListRemovals` | [[!UICONTROL 度量]](./measure.md) | 产品列表中产品条目的删除或删除，如从购物车中删除的产品。 |
| `productListReopens` | [[!UICONTROL 度量]](./measure.md) | 先前已放弃且已被用户重新激活的产品列表。 |
| `productListViews` | [[!UICONTROL 度量]](./measure.md) | 描述产品视图的视图何时发生。 |
| `productViews` | [[!UICONTROL 度量]](./measure.md) | 描述单个产品的视图或视图何时发生。 |
| `purchases` | [[!UICONTROL 度量]](./measure.md) | 用于跟踪何时接受订单。 购买事件是商务转换中唯一必需的操作。 购买事件必须引用产品列表。 |
| `saveForLaters` | [[!UICONTROL 度量]](./measure.md) | 产品列表会保存以备将来使用，如希望列表。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)