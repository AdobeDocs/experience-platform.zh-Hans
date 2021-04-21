---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;geo;circle;datatype;datatype；数据类型；
solution: Experience Platform
title: 地理圈数据类型
topic-legacy: overview
description: 本文档概述了Geo Circle XDM数据类型。
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# [!UICONTROL Geo Circle] 数据类型

[!UICONTROL Geo Circle] 是描述圆形地理区域的标准XDM数据类型，给定以特定坐标集为中心的特定半径。此数据类型基于[模式.org](http://schema.org/GeoCircle)上记录的公共规范。

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | 描述圆心的地理坐标。 |
| `_schema.description` | 字符串 | 圆圈包含的描述。 |
| `_schema.radius` | 双精度 | 圆半径的长度。 此值符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基准，以米为单位测量。 |
| `_id` | 字符串 | 用于圆的唯一、由系统生成的ID。 |
