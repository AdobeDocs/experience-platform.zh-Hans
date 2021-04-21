---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；信标；交互详细信息；数据类型；数据类型；
solution: Experience Platform
title: 地理交互详细信息数据类型
topic-legacy: overview
description: 本文档概述了Geo Interaction Details XDM数据类型。
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 2%

---

# [!UICONTROL Geo interaction details] 数据类型

[!UICONTROL Geo interaction details] 是一种标准XDM数据类型，用于描述地理定义区域中包含的当前状态。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo Shape]](./geo-shape.md) | 描述与之交互的区域的地理形状。 此字段可描述框、圆或多边形。 |
| `deviceGeoAccuracy` | 双精度 | 地球测量设备或机构的精度，以米为单位进行测量。 |
| `distanceToCenter` | 双精度 | 在地球圈的情况下，到地球中心的距离，以米为单位。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
