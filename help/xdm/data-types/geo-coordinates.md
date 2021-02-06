---
keywords: Experience Platform；主题；热门主题；模式;模式;XDM；字段；模式;模式；地理；坐标；数据类型；数据类型；
solution: Experience Platform
title: 地理坐标数据类型
topic: overview
description: 此文档概述了地理坐标XDM数据类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---


# [!UICONTROL 地理] 坐标数据类型

[!UICONTROL 地] 理协调是一种标准XDM数据类型，用于描述地理坐标。此数据类型基于[模式.org](https://schema.org/GeoCoordinates)上记录的公共规范。

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.description` | 字符串 | 坐标标识的描述。 |
| `_schema.elevation` | 双精度 | 已定义坐标的特定高度。 该值必须符合[WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)基准，以米为单位。 |
| `_schema.latitude` | 双精度 | 地理点的已签名垂直坐标。 |
| `_schema.longitude` | 双精度 | 地理点的已签名水平坐标。 |
| `_id` | 字符串 | 坐标的唯一、系统生成的ID。 |
