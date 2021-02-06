---
keywords: Experience Platform；主题；热门主题；模式;模式;XDM；字段；模式;模式；地理；圆；数据类型；数据类型；
solution: Experience Platform
title: 地理圈数据类型
topic: overview
description: 此文档概述了Geo Circle XDM数据类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---


# [!UICONTROL 地理] 循环数据类型

[!UICONTROL Geo Circle] 是一种标准XDM数据类型，它描述圆形地理区域，给定以特定坐标集为中心的特定半径。此数据类型基于[模式.org](http://schema.org/GeoCircle)上记录的公共规范。

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述圆心的地理坐标。 |
| `_schema.description` | 字符串 | 圆圈包含的描述。 |
| `_schema.radius` | 双精度 | 圆的半径长度。 此值符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基准，以米为单位。 |
| `_id` | 字符串 | 用于圆圈的唯一、由系统生成的ID。 |
