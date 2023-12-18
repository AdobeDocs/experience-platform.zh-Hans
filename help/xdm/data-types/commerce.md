---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；商务；数据类型；数据类型；
solution: Experience Platform
title: Commerce数据类型
description: 了解Commerce Experience Data Model (XDM)数据类型。
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!UICONTROL 商务] 数据类型

[!UICONTROL 商务] 是一个标准的体验数据模型(XDM)数据类型，用于描述与购买和销售相关的记录。

![的图表 [!UICONTROL 商务] 数据类型。](../images/data-types/commerce.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL 订购] | `order` | [[!UICONTROL 订购]](./order.md) | 描述一个或多个产品的已下订单。 |
| [!UICONTROL 促销ID] | `promotionID` | [!UICONTROL 字符串] | 已下达订单的促销标识符（如果存在）。 |
| [!UICONTROL 购物车放弃] | `cartAbandons` | [[!UICONTROL 衡量]](./measure.md) | 描述产品列表何时已被标识为用户不再可访问或购买。 |
| [!UICONTROL 结账] | `checkouts` | [[!UICONTROL 衡量]](./measure.md) | 在产品列表的结账过程中执行的操作。 如果结账过程包含多个步骤，则可能有多个结账事件。 如果有多个步骤，则使用事件时间信息和引用的页面或体验来按顺序标识该步骤和各个事件。 |
| [!UICONTROL 产品列表（购物车）添加次数] | `productListAdds` | [[!UICONTROL 衡量]](./measure.md) | 将产品添加到产品列表，例如将产品添加到购物车。 |
| [!UICONTROL 产品列表（购物车）打开] | `productListOpens` | [[!UICONTROL 衡量]](./measure.md) | 新产品列表的初始化，例如正在创建的购物车。 |
| [!UICONTROL 产品列表（购物车）移除次数] | `productListRemovals` | [[!UICONTROL 衡量]](./measure.md) | 从产品列表中删除产品条目，如从购物车中删除的产品。 |
| [!UICONTROL 产品列表（购物车）重新打开] | `productListReopens` | [[!UICONTROL 衡量]](./measure.md) | 用户已重新激活之前放弃的产品列表。 |
| [!UICONTROL 产品列表（购物车）视图] | `productListViews` | [[!UICONTROL 衡量]](./measure.md) | 描述产品列表视图何时发生。产品列表视图何时发生。 |
| [!UICONTROL 产品查看次数] | `productViews` | [[!UICONTROL 衡量]](./measure.md) | 描述单个产品的查看时间。 |
| [!UICONTROL 购买] | `purchases` | [[!UICONTROL 衡量]](./measure.md) | 用于跟踪订单何时被接受。 在商业转化中，购买事件是唯一所需的操作。 购买事件必须具有引用的产品列表。 |
| [!UICONTROL 保存留待后用] | `saveForLaters` | [[!UICONTROL 衡量]](./measure.md) | 描述何时保存产品列表以供将来使用，例如希望列表。 |
| [!UICONTROL 店内购买] | `inStorePurchase` | [[!UICONTROL 衡量]](./measure.md) | 指示“inStore”购买。 保存此信息以供分析使用。 |
| [!UICONTROL 购物车] | `cart` | [[!UICONTROL 购物车]](./cart.md) | 包含一个或多个产品的购物车的属性。 |
| [!UICONTROL 配送] | `shipping` | [[!UICONTROL 配送]](./shipping.md) | 一个或多个产品的运输详细信息。 |
| [!UICONTROL 帐单] | `billing` | [[!UICONTROL 计费]](#billing) | 一项或多项付款的计费详细信息。 |
| [!UICONTROL 即时购买] | `instantPurchase` | [[!UICONTROL 衡量]](./measure.md) | 描述何时即时购买产品，可能跳过购物车或结账。 |
| [!UICONTROL 申请列表打开] | `requisitionListOpens` | [[!UICONTROL 衡量]](./measure.md) | 指示新申请列表的初始化。 |
| [!UICONTROL 申请列表删除] | `requisitionListDeletes` | [[!UICONTROL 衡量]](./measure.md) | 指示删除申请列表。 |
| [!UICONTROL 申请列表添加] | `requisitionListAdds` | [[!UICONTROL 衡量]](./measure.md) | 指示将产品添加到申请列表。 |
| [!UICONTROL 申请列表移除次数] | `requisitionListRemovals` | [[!UICONTROL 衡量]](./measure.md) | 指示从申请产品列表中删除产品。 |
| [!UICONTROL 需求列表] | `requisitionList` | [[!UICONTROL requisitionlist]](./requisition-list.md) | 客户创建的申请列表的属性。 |
| [!UICONTROL 范围] | `commerceScope` | [[!UICONTROL Commercescope]](./commerce-scope.md) | 发生事件的位置的商业范围标识符（商店视图、商店、网站等）。 |

{style="table-layout:auto"}

## [!UICONTROL 计费] 数据类型 {#billing}

[!UICONTROL 计费] 是一个标准的体验数据模型(XDM)数据类型，其中包含有关计费详细信息的信息。 具体来说，它侧重于账单地址。

![计费数据类型的图表。](../images/data-types/billing.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL 帐单地址] | `address` | [[!UICONTROL 邮政地址]](./postal-address.md) | 帐单地址。 |

{style="table-layout:auto"}

欲知关于 [!UICONTROL 商务] 数据类型，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
