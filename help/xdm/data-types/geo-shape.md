---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;geo shape;datatype;data-type;data type;
solution: Experience Platform
title: 地理形状数据类型
topic: overview
description: 此文档概述了Geo Shape XDM数据类型。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---


# [!UICONTROL 地理形状] 数据类型

[!UICONTROL Geo Shape是] 一种标准XDM数据类型，用于描述地理区域的形状。 此数据类型基于模式.org上记录的公 [共规范](https://schema.org/GeoShape)。

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.box` | 地理坐 [[!UICONTROL 标阵列]](./geo-coordinates.md) | 描述由两个坐标构成的矩形包围的地理区域。 第一个坐标是矩形的下角，第二个坐标是上角。 |
| `_schema.circle` | 地理坐 [[!UICONTROL 标阵列]](./geo-coordinates.md) | 描述具有以地理坐标为中心的特定半径的圆形区域。 |
| `_schema.polygon` | [[!UICONTROL 地理圈]](./geo-circle.md) | 一系列四个或更多坐标，其中第一个和最后一个坐标相同。 |
| `_schema.description` | 字符串 | 形状的定义描述。 |
| `_schema.elevation` | 双精度 | 形状的特定或最小高度。 此值符合WGS84 [基准](http://gisgeography.com/wgs84-world-geodetic-system/) ，以米为单位。 与之结 `ceiling`合，此属性可用于表示位置的三维定界框。 |
| `_id` | 字符串 | 形状的唯一、由系统生成的标识符。 |
| `ceiling` | 双精度 | 形状的最大高度。 此属性仅在与结合使用时有效 `elevation`。 该值符合WGS84 [基准](http://gisgeography.com/wgs84-world-geodetic-system/) ，以米为单位。 与之结 `elevation`合，此属性可用于表示位置的三维定界框。 |
