---
title: Advertising Pod详细信息报表数据类型
description: 了解Advertising Pod Details Reporting Experience Data Model (XDM)数据类型。
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# [!UICONTROL Advertising Pod详细信息报告]数据类型

[!UICONTROL Advertising Pod Details Reporting]是标准的Experience Data Model (XDM)数据类型。 它定义了一个序列或一组广告，通常在内容中断期间连续播放。 使用[!UICONTROL Advertising面板详细信息报表]数据类型可捕获详细信息，如广告时间ID、广告时间的友好名称、广告时间内的广告索引以及内容时间线内广告时间的偏移（以秒为单位）。

![Advertising面板详细信息报表数据类型的图表。](../images/data-types/advertising-pod-details-information.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 广告时间ID] | `ID` | 字符串 | 广告时间的ID。 |
| [!UICONTROL Pod友好名称] | `friendlyName` | 字符串 | 广告时间的易于理解的名称。 |
| [!UICONTROL 面板中的广告位置] | `index` | 整数 | 父广告时间开始内的广告索引。 |
| [!UICONTROL Pod偏移] | `offset` | 整数 | **必需**&#x200B;广告时间在内容中的偏移，以秒为单位。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
