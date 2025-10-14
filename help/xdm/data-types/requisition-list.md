---
title: 申购单列表数据类型
description: 了解申请列表体验数据模型(XDM)数据类型。
exl-id: cbea6b08-9d4d-4cbe-b0c5-506bccc6df67
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 7%

---

# [!UICONTROL 申请列表]数据类型

[!UICONTROL 申请列表]是标准的体验数据模型(XDM)数据类型，用于描述采购或采购项目的策划集合。 使用[!UICONTROL 申请列表]数据类型识别和描述申请列表。

![&#x200B; [!UICONTROL 申请列表]数据类型的图表。](../images/data-types/requisition-list.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL 申请列表ID] | `ID` | 字符串 | 申购单列表的唯一标识符。 |
| [!UICONTROL 申请列表名称] | `name` | 字符串 | 客户指定的申请列表的名称。 |
| [!UICONTROL 申购单列表说明] | `description` | 字符串 | 客户指定的申请列表的描述。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
