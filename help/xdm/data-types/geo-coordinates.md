---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；地理；坐标；数据类型；数据类型；
solution: Experience Platform
title: 地理坐标数据类型
topic-legacy: overview
description: 本文档概述了地理坐标XDM数据类型。
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

# [!UICONTROL Geo Coordinates] 数据类型

[!UICONTROL Geo Coordinates] 是描述地理坐标的标准XDM数据类型。此数据类型基于[模式.org](https://schema.org/GeoCoordinates)上记录的公共规范。

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.description` | 字符串 | 坐标标识的描述。 |
| `_schema.elevation` | 双精度 | 已定义坐标的特定仰角。 该值必须符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基准，以米为单位。 |
| `_schema.latitude` | 双精度 | 地理点的符号垂直坐标。 |
| `_schema.longitude` | 双精度 | 地理点的带符号的水平坐标。 |
| `_id` | 字符串 | 坐标的唯一、由系统生成的ID。 |
