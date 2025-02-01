---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地域；地理形状；数据类型；数据类型；
solution: Experience Platform
title: 地理形状数据类型
description: 了解地理形状XDM数据类型。
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# [!UICONTROL 地理形状]数据类型

[!UICONTROL 地理形状]是描述地理区域形状的标准XDM数据类型。 此数据类型基于[schema.org](https://schema.org/GeoShape)上记录的公共规范。

![](../images/data-types/geo-shape.png){width=500}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.box` | [[!UICONTROL 地理坐标的数组]](./geo-coordinates.md) | 描述由两个坐标形成的矩形包围的地理区域。 第一个坐标是矩形的下角，第二个坐标是上角。 |
| `_schema.circle` | [[!UICONTROL 地理坐标的数组]](./geo-coordinates.md) | 描述以地理坐标为中心的具有特定半径的圆形区域。 |
| `_schema.polygon` | [[!UICONTROL 地理圈]](./geo-circle.md) | 四个或更多坐标的系列，其中第一个坐标和最后一个坐标相同。 |
| `_schema.description` | 字符串 | 形状定义的内容的描述。 |
| `_schema.elevation` | 双精度 | 形状的特定或最小标高。 此值符合[WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)基准，以米为测量单位。 在与`ceiling`结合使用时，此属性可用于表示位置的三维边界框。 |
| `_id` | 字符串 | 形状的系统生成的唯一标识符。 |
| `ceiling` | 双精度 | 形状的最大标高。 此属性仅在与`elevation`结合使用时有效。 该值符合[WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)基准，以米为测量单位。 在与`elevation`结合使用时，此属性可用于表示位置的三维边界框。 |
