---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;poi;poi详细信息；关注点；兴趣点详细信息；数据类型；数据类型；
solution: Experience Platform
title: 兴趣点详细信息数据类型
topic-legacy: overview
description: 本文档概述了兴趣点详细信息XDM数据类型。
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 4%

---

# [!UICONTROL Point of interest details] 数据类型

[!UICONTROL Point of interest details] 是一种标准XDM数据类型，用于描述在其中观察到事件的地理相关数据。

<img src="../images/data-types/poi-details.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | 描述POI交互活动的信标详细信息。 |
| `geoInteractionDetails` | [[!UICONTROL Geo interaction details]](./geo-interaction-details.md) | 描述POI交互活动的地理详细信息。 |
| `category` | 字符串 | 由POI定义的管理员分配用于组织POI的常规类别。 |
| `distanceToPOICenter` | 双精度 | POI中心的估计距离（以米为单位）。 |
| `locatingType` | 字符串 | 用于确定位置的机制。 接受的值包括： <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 字符串 | 给POI的名字。 |
| `poiID` | 字符串 | POI的唯一标识符。 |
| `type` | 字符串 | 使用由POI定义的管理员选择的键入模式的POI的常规类型。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
