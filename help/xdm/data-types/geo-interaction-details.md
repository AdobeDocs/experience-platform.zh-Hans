---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: 地理交互详细信息数据类型
topic: overview
description: 此文档概述了Geo Interaction Details XDM数据类型。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# [!UICONTROL 地理交互详细信息] （数据类型）

[!UICONTROL 地理交互详细信息] 是一种标准的XDM数据类型，用于描述地理定义区域中包含的当前状态。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 地理形状]](./geo-shape.md) | 描述所交互的区域的地理形状。 此字段可以描述框、圆或多边形。 |
| `deviceGeoAccuracy` | 双精度 | 地质测量设备或机构的精度，以米为单位进行测量。 |
| `distanceToCenter` | 双精度 | 在地理圈中到地理中心的距离，以米为单位。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
