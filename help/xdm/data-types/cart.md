---
title: 购物车数据类型
description: 了解Cart Experience Data Model (XDM)数据类型。
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 5%

---

# [!UICONTROL 购物车] 数据类型

[!UICONTROL 购物车] 是一个标准体验数据模型(XDM)数据类型，它提供与购物车相关的属性。 使用此数据类型捕获卖方分配的唯一标识符(`Cart ID`)和源(`Cart Source`)将一个或多个产品添加到购物车中。

![的图表 [!UICONTROL 购物车] 数据类型。](../images/data-types/cart.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL 购物车Id] | `cartID` | 字符串 | 卖方为购物车分配的唯一标识符。 |
| [!UICONTROL 购物车来源] | `cartSource` | 字符串 | 将一个或多个产品添加到购物车的位置。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
