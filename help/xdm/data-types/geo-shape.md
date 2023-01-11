---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地理；地理形状；数据类型；数据类型；
solution: Experience Platform
title: 地理形状数据类型
description: 本文档概述了地理形状XDM数据类型。
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# [!UICONTROL 地理形状] 数据类型

[!UICONTROL 地理形状] 是描述地理区域形状的标准XDM数据类型。 此数据类型基于 [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.box` | 数组 [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述由两个坐标组成的矩形包围的地理区域。 第一坐标是矩形的下角，第二坐标是上角。 |
| `_schema.circle` | 数组 [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述以地理坐标为中心的特定半径的圆形区域。 |
| `_schema.polygon` | [[!UICONTROL 地域圈子]](./geo-circle.md) | 一系列四个或更多坐标，其中第一个坐标和最后一个坐标是相同的。 |
| `_schema.description` | 字符串 | 形状的定义描述。 |
| `_schema.elevation` | 双精度 | 形状的特定高度或最小高度。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基准和以米为单位测量。 与 `ceiling`，此属性可用于表示位置的三维定界框。 |
| `_id` | 字符串 | 形状的唯一、系统生成的标识符。 |
| `ceiling` | 双精度 | 形状的最大高度。 仅当与 `elevation`. 值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基准和以米为单位测量。 与 `elevation`，此属性可用于表示位置的三维定界框。 |
