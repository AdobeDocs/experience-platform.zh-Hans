---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；信标；交互详细信息；数据类型；数据类型；
solution: Experience Platform
title: 地域交互详细信息数据类型
description: 本文档概述了地域交互详细信息XDM数据类型。
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 4%

---

# [!UICONTROL 地域交互详细信息] 数据类型

[!UICONTROL 地域交互详细信息] 是一种标准的XDM数据类型，用于描述在地理上定义的区域中包含的当前状态。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 地理形状]](./geo-shape.md) | 描述所交互的区域的地理形状。 此字段可描述框、圆或多边形。 |
| `deviceGeoAccuracy` | 双精度 | 以米为单位测量的地域测量设备或机构的精度。 |
| `distanceToCenter` | 双精度 | 在地域圆的情况下，到地域中心的距离（以米为单位）。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
