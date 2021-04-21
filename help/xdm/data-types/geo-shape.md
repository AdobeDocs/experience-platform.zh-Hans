---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;geo;geo形状；datatype;datatype；数据类型；
solution: Experience Platform
title: 地理形状数据类型
topic-legacy: overview
description: 本文档概述了Geo Shape XDM数据类型。
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 2%

---

# [!UICONTROL Geo Shape] 数据类型

[!UICONTROL Geo Shape] 是描述地理区域形状的标准XDM数据类型。此数据类型基于[模式.org](https://schema.org/GeoShape)上记录的公共规范。

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.box` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md)的数组 | 描述由两个坐标组成的矩形所包围的地理区域。 第一个坐标是矩形的下角，第二个坐标是上角。 |
| `_schema.circle` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md)的数组 | 描述以地理坐标为中心的特定半径的圆形区域。 |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | 一系列四个或更多坐标，其中第一个和最终坐标相同。 |
| `_schema.description` | 字符串 | 形状定义的描述。 |
| `_schema.elevation` | 双精度 | 形状的特定或最小高度。 此值符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基准，以米为单位测量。 与`ceiling`结合使用，此属性可用于表示位置的三维边框。 |
| `_id` | 字符串 | 形状的唯一、系统生成的标识符。 |
| `ceiling` | 双精度 | 形状的最大高度。 仅当与`elevation`结合使用时，此属性才有效。 该值符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基准，以米为单位测量。 与`elevation`结合使用，此属性可用于表示位置的三维边框。 |
