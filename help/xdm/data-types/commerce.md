---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；商务；数据类型；数据类型；
solution: Experience Platform
title: 商务数据类型
description: 本文档概述了商务体验数据模型(XDM)数据类型。
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL 商务] 数据类型

[!UICONTROL 商务] 是一种标准的体验数据模型(XDM)数据类型，用于描述与购买和销售活动相关的记录。

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `order` | [[!UICONTROL 订购]](./order.md) | 描述一个或多个产品的下单。 |
| `cartAbandons` | [[!UICONTROL 测量]](./measure.md) | 用于描述产品列表何时被标识为不再可供用户访问或购买。 |
| `checkouts` | [[!UICONTROL 测量]](./measure.md) | 产品列表结账过程中的操作。 如果结帐流程中存在多个步骤，则可能会有多个结帐事件。 如果有多个步骤，则会使用事件时间信息以及引用的页面或体验来标识按顺序表示的步骤和各个事件。 |
| `inStorePurchase` | [[!UICONTROL 测量]](./measure.md) | 描述与供Analytics使用的店内购买关联的值。 |
| `productListAdds` | [[!UICONTROL 测量]](./measure.md) | 产品列表中添加的产品，例如添加到购物车的产品。 |
| `productListOpens` | [[!UICONTROL 测量]](./measure.md) | 新产品列表的初始化，如正在创建的购物车。 |
| `productListRemovals` | [[!UICONTROL 测量]](./measure.md) | 产品列表中产品条目的移除或移除，例如从购物车移除的产品。 |
| `productListReopens` | [[!UICONTROL 测量]](./measure.md) | 先前已放弃且用户已重新激活的产品列表。 |
| `productListViews` | [[!UICONTROL 测量]](./measure.md) | 描述产品列表的视图或视图何时发生。 |
| `productViews` | [[!UICONTROL 测量]](./measure.md) | 描述单个产品的视图或视图何时发生。 |
| `purchases` | [[!UICONTROL 测量]](./measure.md) | 用于跟踪何时接受订单。 购买事件是商务转化中唯一必需的操作。 购买事件必须引用产品列表。 |
| `saveForLaters` | [[!UICONTROL 测量]](./measure.md) | 保存产品列表供将来使用，如愿望列表。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
