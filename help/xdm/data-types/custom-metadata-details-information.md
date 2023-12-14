---
title: 自定义元数据详细信息数据类型
description: 了解自定义元数据详细信息体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# [!UICONTROL 自定义元数据详细信息] 数据类型

[!UICONTROL 自定义元数据详细信息] 是一个标准体验数据模型(XDM)数据类型，它定义了用于存储自定义元数据的结构。 使用 [!UICONTROL 自定义元数据详细信息] 用于捕获详细信息（如与内容或交互关联的自定义元数据的名称和值）的数据类型。

![自定义元数据详细信息数据类型的图表。](../images/data-types/custom-metadata-details-information.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL 自定义元数据字段名称] | `name` | 字符串 | 自定义字段的名称。 |
| [!UICONTROL 自定义元数据字段值] | `value` | 字符串 | 自定义字段的值。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
