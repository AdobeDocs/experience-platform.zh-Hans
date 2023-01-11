---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地理；坐标；数据类型；数据类型；
solution: Experience Platform
title: 地理坐标数据类型
description: 本文档概述了地理坐标XDM数据类型。
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL 地理坐标] 数据类型

[!UICONTROL 地理坐标] 是描述位置地理坐标的标准XDM数据类型。 此数据类型基于 [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.description` | 字符串 | 坐标的标识描述。 |
| `_schema.elevation` | 双精度 | 定义坐标的特定高度。 值必须符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基准和以米为单位测量。 |
| `_schema.latitude` | 双精度 | 地理点的带符号的垂直坐标。 |
| `_schema.longitude` | 双精度 | 地理点的带符号的水平坐标。 |
| `_id` | 字符串 | 坐标的唯一、系统生成的ID。 |
