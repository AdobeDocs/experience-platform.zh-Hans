---
title: 购物车数据类型
description: 了解Cart Experience Data Model (XDM)数据类型。
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 14%

---

# [!UICONTROL 购物车]数据类型

[!UICONTROL 购物车]是一种标准体验数据模型(XDM)数据类型，它提供与购物车相关的属性。 使用此数据类型捕获由销售方(`Cart ID`)和源(`Cart Source`)分配的唯一标识符，其中一个或多个产品已添加到购物车。

![&#x200B; [!UICONTROL 购物车]数据类型的图表。](../images/data-types/cart.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL 购物车ID] | `cartID` | 字符串 | 卖方为购物车分配的唯一标识符。 |
| [!UICONTROL 购物车Source] | `cartSource` | 字符串 | 将一个或多个产品添加到购物车的位置。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
