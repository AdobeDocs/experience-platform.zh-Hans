---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinates;datatype;data-type;data type;
solution: Experience Platform
title: 地理坐标数据类型
topic: overview
description: 此文档概述了地理坐标XDM数据类型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---


# [!UICONTROL 地理坐标] 数据类型

[!UICONTROL Geo Coordinates] 是一种标准XDM数据类型，用于描述地理坐标。 此数据类型基于模式.org上记录的公 [共规范](https://schema.org/GeoCoordinates)。

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.description` | 字符串 | 坐标标识的描述。 |
| `_schema.elevation` | 双精度 | 已定义坐标的特定高度。 该值必须符合WGS84 [基准](http://gisgeography.com/wgs84-world-geodetic-system/) ，以米为单位。 |
| `_schema.latitude` | 双精度 | 地理点的已签名垂直坐标。 |
| `_schema.longitude` | 双精度 | 地理点的已签名水平坐标。 |
| `_id` | 字符串 | 坐标的唯一、系统生成的ID。 |
