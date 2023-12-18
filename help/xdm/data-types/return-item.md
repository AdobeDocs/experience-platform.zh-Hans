---
title: 返回项数据类型
description: 了解退货项目体验数据模型(XDM)数据类型。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# [!UICONTROL 返回项目] 数据类型

[!UICONTROL 返回项目] 是一个标准体验数据模型(XDM)数据类型，可捕获与购买项目的退货流程相关的重要详细信息。

![返回项数据类型的图表。](../images/data-types/return-item.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL 返回状态] | `returnStatus` | 字符串 | 返回项目的状态（例如，“待定”或“已批准”）。 |
| [!UICONTROL 退货原因] | `returnReason` | 字符串 | 要求返回物料的原因。 |
| [!UICONTROL 退货条件] | `returnItemCondition` | 字符串 | 请求返回的项目的条件。 |
| [!UICONTROL 返回分辨率] | `returnResolution` | 字符串 | 从退货中期望的解决方法或结果（例如，退款或兑换）。 |
| [!UICONTROL 请求的退货数量] | `returnQuantityRequested` | 整数 | 购物者请求退回的物料数量。 |
| [!UICONTROL 已授权的退货数量] | `returnQuantityAuthorized` | 整数 | 授权退回的物料数量。 |
| [!UICONTROL 退货接收数量] | `returnQuantityReceived` | 整数 | 收到的退回物料的数量。 |
| [!UICONTROL 已批准的退货数量] | `returnQuantityApproved` | 整数 | 退货完全完成并批准的物料数量。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)
