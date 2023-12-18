---
title: 申购单列表数据类型
description: 了解申请列表体验数据模型(XDM)数据类型。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 5%

---

# [!UICONTROL 申请列表] 数据类型

[!UICONTROL 申请列表] 是一个标准体验数据模型(XDM)数据类型，用于描述为采购或购买策划的项集合。 使用 [!UICONTROL 申请列表] 用于标识和描述申请列表的数据类型。

![的图表 [!UICONTROL 申请列表] 数据类型。](../images/data-types/requisition-list.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL 申购单列表ID] | `ID` | 字符串 | 申购单列表的唯一标识符。 |
| [!UICONTROL 申购单列表名称] | `name` | 字符串 | 客户指定的申请列表的名称。 |
| [!UICONTROL 申购单列表说明] | `description` | 字符串 | 客户指定的申请列表的描述。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
