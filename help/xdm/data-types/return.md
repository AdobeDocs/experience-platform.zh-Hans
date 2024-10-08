---
title: 返回数据类型
description: 了解回访体验数据模型(XDM)数据类型。
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 8%

---

# [!UICONTROL 返回]数据类型

[!UICONTROL Return]是一种标准的体验数据模型(XDM)数据类型，可捕获与退货商品授权(RMA)相关的基本信息。

![返回数据类型的图表。](../images/data-types/return.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL 返回ID] | `returnID` | 字符串 | 此RMA的唯一标识符。 |
| [!UICONTROL 返回状态] | `returnStatus` | 字符串 | RMA的当前状态（例如“待定”或“已关闭”）。 |
| [!UICONTROL 订单购买ID] | `purchaseID` | 字符串 | RMA所属的订单/购买的唯一标识符。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)
