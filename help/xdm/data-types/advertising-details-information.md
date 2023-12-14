---
title: 广告详细信息数据类型
description: 了解广告详细信息体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 11%

---

# [!UICONTROL 广告详细信息] 数据类型

[!UICONTROL 广告详细信息] 是一种标准的体验数据模型(XDM)数据类型，可捕获与广告相关的关键属性。 其中包括广告ID、广告商和促销活动ID、长度、序列中的位置、有关播放器呈现广告的详细信息等信息。 您可以使用此数据类型跟踪和分析广告效果和参与度的各个方面，并提供受众如何与不同广告进行交互和做出响应的洞察。

+++选择以显示广告详细信息数据类型的图表。
![广告详细信息数据类型的图表。](../images/data-types/advertising-details-information.png)
+++

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL 广告名称] | `friendlyName` | 字符串 | **必填** 易于用户识别的广告名称。 在报表中，“广告名称”是分类，“广告名称（变量）”是 eVar。 |
| [!UICONTROL 广告ID] | `name` | 字符串 | 广告的ID。 任何整数和/或字母组合 |
| [!UICONTROL 广告时长或持续时间] | `length` | 整数 | **必填** 视频广告的长度，以秒为单位。 |
| [!UICONTROL 面板中的广告位置（广告开始）] | `podPosition` | 整数 | **必填** 父广告开始内部的广告索引，例如，第一个广告的索引为0，第二个广告的索引为1。 |
| [!UICONTROL 广告播放器名称] | `playerName` | 字符串 | **必填** 负责呈现广告的播放器的名称。 |
| [!UICONTROL 广告商] | `advertiser` | 字符串 | 广告中展现的产品所属的公司或品牌。 |
| [!UICONTROL 广告营销活动] | `campaignID` | 字符串 | 广告营销活动的ID。 |
| [!UICONTROL 广告创意ID] | `creativeID` | 字符串 | 广告创意的ID。 |
| [!UICONTROL 广告网站ID] | `siteID` | 字符串 | 广告网站的ID。 |
| [!UICONTROL 广告创意URL] | `creativeURL` | 字符串 | 广告创意的URL。 |
| [!UICONTROL 广告投放ID] | `placementID` | 字符串 | 广告的版面ID。 |
| [!UICONTROL 广告已完成] | `isCompleted` | 布尔 | 跟踪广告是否已完成。 |
| [!UICONTROL 广告开始] | `isStarted` | 布尔 | 跟踪广告是否已开始。 |
| [!UICONTROL 广告播放时间] | `timePlayed` | 整数 | 观看广告所花费的总时间，以秒为单位（即播放广告所用的秒数）。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
