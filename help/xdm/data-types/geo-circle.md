---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地域；圆；数据类型；数据类型；
solution: Experience Platform
title: 地理圆圈数据类型
description: 本文档概述了Geo Circle XDM数据类型。
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL 地理圈] 数据类型

[!UICONTROL 地理圈] 是描述圆形地理区域的标准XDM数据类型，给定以特定坐标集为中心的特定半径。 此数据类型基于上记录的公共规范 [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述圆心的地理坐标。 |
| `_schema.description` | 字符串 | 圆圈包含的内容的描述。 |
| `_schema.radius` | 双精度 | 圆半径的长度。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基准，以米为测量单位。 |
| `_id` | 字符串 | 系统生成的圆的唯一标识。 |
