---
title: Advertising Pod详细信息报表数据类型
description: 了解Advertising Pod Details Reporting Experience Data Model (XDM)数据类型。
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# [!UICONTROL 广告面板详细信息报表] 数据类型

[!UICONTROL 广告面板详细信息报表] 是标准的体验数据模型(XDM)数据类型。 它定义了一个序列或一组广告，通常在内容中断期间连续播放。 使用 [!UICONTROL 广告面板详细信息报表] 用于捕获详细信息的数据类型，例如广告时间ID、广告时间的友好名称、广告时间内的广告索引以及内容时间轴内广告时间的偏移（以秒为单位）。

![广告面板详细信息报表数据类型的图表。](../images/data-types/advertising-pod-details-information.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 广告时间ID] | `ID` | 字符串 | 广告时间的ID。 |
| [!UICONTROL Pod友好名称] | `friendlyName` | 字符串 | 广告时间的易于理解的名称。 |
| [!UICONTROL 面板中的广告位置] | `index` | 整数 | 父广告时间开始内的广告索引。 |
| [!UICONTROL Pod偏移] | `offset` | 整数 | **必填** 广告时间在内容中的偏移，以秒为单位。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
