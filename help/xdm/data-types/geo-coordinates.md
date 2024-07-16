---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地域；坐标；数据类型；数据类型；
solution: Experience Platform
title: 地理坐标数据类型
description: 了解地理坐标XDM数据类型。
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 13%

---

# [!UICONTROL 地理坐标]数据类型

[!UICONTROL 地理坐标]是描述位置地理坐标的标准XDM数据类型。 此数据类型基于[schema.org](https://schema.org/GeoCoordinates)上记录的公共规范。

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.description` | 字符串 | 坐标标识的内容的描述。 |
| `_schema.elevation` | 两次 | 定义的坐标的特定高程。 该值必须符合[WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)基准，并以米为单位进行测量。 |
| `_schema.latitude` | 两次 | 地理点的带符号垂直坐标。 |
| `_schema.longitude` | 两次 | 地理点的带符号水平坐标。 |
| `_id` | 字符串 | 系统生成的唯一坐标ID。 |
