---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data-type;data type;
solution: Experience Platform
title: 地理圈数据类型
topic: overview
description: 此文档概述了Geo Circle XDM数据类型。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 4%

---


# [!UICONTROL Geo Circle数据] 类型

[!UICONTROL Geo Circle] 是一种标准XDM数据类型，它描述圆形地理区域，给定以特定坐标集为中心的特定半径。 此数据类型基于模式.org上记录的公 [共规范](http://schema.org/GeoCircle)。

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述圆心的地理坐标。 |
| `_schema.description` | 字符串 | 圆圈包含的描述。 |
| `_schema.radius` | 双精度 | 圆的半径长度。 此值符合WGS84 [基准](http://gisgeography.com/wgs84-world-geodetic-system/) ，以米为单位。 |
| `_id` | 字符串 | 用于圆圈的唯一、由系统生成的ID。 |
