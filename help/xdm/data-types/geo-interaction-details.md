---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；信标；交互详细信息；数据类型；数据类型；
solution: Experience Platform
title: 地理位置交互详细信息数据类型
description: 了解地域交互详细信息XDM数据类型。
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 13%

---

# [!UICONTROL 地理位置交互详细信息]数据类型

[!UICONTROL 地理位置交互详细信息]是一种标准XDM数据类型，它描述了地理位置定义的区域中包含的当前状态。

![](../images/data-types/geo-interaction-details.png){width=400}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 地理形状]](./geo-shape.md) | 描述与之交互的区域的地理形状。 此字段可描述框、圆或多边形。 |
| `deviceGeoAccuracy` | 双精度 | 地理测量设备或机构的精度（以米为单位）。 |
| `distanceToCenter` | 双精度 | 在圆形地理区域的情况下与地理中心的距离（以米为单位）。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
