---
title: 错误详细信息数据类型
description: 了解错误详细信息体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 5%

---

# [!UICONTROL 错误详细信息] 数据类型

[!UICONTROL 错误详细信息] 是一个标准体验数据模型(XDM)数据类型，用于描述错误详细信息。 使用 [!UICONTROL 错误详细信息] 用于捕获错误源和标识的详细资料的数据类型。 错误ID标识错误，并且错误源指定它来自播放器还是外部源。

![错误详细信息数据类型的图表。](../images/data-types/error-details-information.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL 错误Id] | `name` | 字符串 | 错误ID |
| [!UICONTROL 错误源] | `source` | 字符串 | 错误源。 已枚举：“player”、“external”以及各自的含义。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
