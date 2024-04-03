---
title: Advertising Pod详细信息收集数据类型
description: 了解Advertising Pod Details Collection Experience Data Model (XDM)数据类型。
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---

# [!UICONTROL Advertising Pod详细信息] 收藏集数据类型

[!UICONTROL Advertising Pod详细信息] 收藏集是一种标准的体验数据模型(XDM)数据类型。 它定义了一个序列或一组广告，通常在内容中断期间连续播放。 使用 [!UICONTROL Advertising Pod详细信息] 用于捕获详细信息的收集数据类型，例如广告时间ID、广告时间的友好名称、广告时间内的广告索引以及内容时间轴内广告时间的偏移（以秒为单位）。

![广告面板详细信息收集数据类型的图表。](../images/data-types/advertising-pod-details-collection.png)

| 显示名称 | 属性 | 数据类型 | 必需 | 描述 |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL 面板中的广告位置] | `index` | 整数 | 是 | 父广告时间开始内的广告索引。 |
| [!UICONTROL Pod友好名称] | `friendlyName` | 字符串 | 否 | 广告时间的易于理解的名称。 |
| [!UICONTROL Pod偏移] | `offset` | 整数 | 是 | 广告时间在内容中的偏移，以秒为单位。 |
