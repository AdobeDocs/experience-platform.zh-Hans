---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；地域；圈子；数据类型；数据类型；
solution: Experience Platform
title: 地域圈数据类型
description: 本文档概述了地域圈子XDM数据类型。
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL 地域圈子] 数据类型

[!UICONTROL 地域圈子] 是描述圆形地理区域的标准XDM数据类型，给定的特定半径以特定坐标集为中心。 此数据类型基于 [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL 地理坐标]](./geo-coordinates.md) | 描述圆心的地理坐标。 |
| `_schema.description` | 字符串 | 对圈子所包含内容的描述。 |
| `_schema.radius` | 双精度 | 圆半径的长度。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基准和以米为单位测量。 |
| `_id` | 字符串 | 圈子的唯一、系统生成的ID。 |
