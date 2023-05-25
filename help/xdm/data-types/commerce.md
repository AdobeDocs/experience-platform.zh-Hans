---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；商务；数据类型；数据类型；
solution: Experience Platform
title: Commerce数据类型
description: 本文档概述了Commerce Experience Data Model (XDM)数据类型。
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL 商务] 数据类型

[!UICONTROL 商务] 是一个标准体验数据模型(XDM)数据类型，用于描述与购买和销售活动相关的记录。

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `order` | [[!UICONTROL 订购]](./order.md) | 描述一个或多个产品的已下订单。 |
| `cartAbandons` | [[!UICONTROL 衡量]](./measure.md) | 用于描述产品列表何时被标识为用户不再可访问或购买。 |
| `checkouts` | [[!UICONTROL 衡量]](./measure.md) | 在产品列表的结账过程中执行的操作。 如果结账过程包含多个步骤，则可能有多个结账事件。 如果有多个步骤，则使用事件时间信息和引用的页面或体验来按顺序标识步骤和各个事件。 |
| `inStorePurchase` | [[!UICONTROL 衡量]](./measure.md) | 描述与店内购买关联的值，以供分析使用。 |
| `productListAdds` | [[!UICONTROL 衡量]](./measure.md) | 将产品添加到产品列表，例如将产品添加到购物车。 |
| `productListOpens` | [[!UICONTROL 衡量]](./measure.md) | 新产品列表的初始化，例如正在创建的购物车。 |
| `productListRemovals` | [[!UICONTROL 衡量]](./measure.md) | 从产品列表中删除产品条目，例如从购物车中删除的产品。 |
| `productListReopens` | [[!UICONTROL 衡量]](./measure.md) | 用户已重新激活之前放弃的产品列表。 |
| `productListViews` | [[!UICONTROL 衡量]](./measure.md) | 描述何时发生产品列表查看。 |
| `productViews` | [[!UICONTROL 衡量]](./measure.md) | 描述何时出现单个产品的查看事件。 |
| `purchases` | [[!UICONTROL 衡量]](./measure.md) | 用于跟踪订单何时被接受。 购买事件是商务转换中唯一需要的操作。 购买事件必须具有引用的产品列表。 |
| `saveForLaters` | [[!UICONTROL 衡量]](./measure.md) | 保存产品列表以供将来使用，例如希望列表。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
