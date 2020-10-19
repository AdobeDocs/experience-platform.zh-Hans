---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;poi details;point of interest;point of interest details;datatype;data-type;data type;
solution: Experience Platform
title: 兴趣点详细信息数据类型
topic: overview
description: 此文档概述了兴趣点详细信息XDM数据类型。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 4%

---


# [!UICONTROL 兴趣点详细信息] ，数据类型

[!UICONTROL 兴趣点详细信息] 是一种标准XDM数据类型，用于描述在其中观察到事件的地理相关数据。

<img src="../images/data-types/poi-details.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL 信标]](./beacon.md) | 描述POI交互中处于活动状态的信标详细信息。 |
| `geoInteractionDetails` | [[!UICONTROL 地理交互详细信息]](./geo-interaction-details.md) | 描述POI交互中处于活动状态的地理详细信息。 |
| `category` | 字符串 | 由POI定义的管理员分配用于组织POI的常规类别。 |
| `distanceToPOICenter` | 双精度 | 距离POI中心的估计距离（以米为单位）。 |
| `locatingType` | 字符串 | 用于确定位置的机制。 接受的值包括： <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 字符串 | 给POI的名字。 |
| `poiID` | 字符串 | POI的唯一标识符。 |
| `type` | 字符串 | 使用由POI定义的管理员选择的键入模式符的POI的常规类型。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)