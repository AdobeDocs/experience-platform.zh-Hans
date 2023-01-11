---
keywords: Experience Platform；主页；热门主题；架构；XDM；字段；架构；架构；poi;poi详细信息；目标点；兴趣点详细信息；数据类型；数据类型；
solution: Experience Platform
title: 目标点详细信息数据类型
description: 本文档概述了兴趣点详细信息XDM数据类型。
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 5%

---

# [!UICONTROL 目标点详细信息] 数据类型

[!UICONTROL 目标点详细信息] 是一种标准的XDM数据类型，用于描述在其中观察到事件的与地理相关的数据。

<img src="../images/data-types/poi-details.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL 信标]](./beacon.md) | 描述POI交互中处于活动状态的信标详细信息。 |
| `geoInteractionDetails` | [[!UICONTROL 地域交互详细信息]](./geo-interaction-details.md) | 描述POI交互中活动的地域详细信息。 |
| `category` | 字符串 | 由POI定义的管理员分配用于组织POI的常规类别。 |
| `distanceToPOICenter` | 双精度 | 距POI中心的估计距离（以米为单位）。 |
| `locatingType` | 字符串 | 用于确定位置的机制。 接受的值包括： <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 字符串 | 给POI的名称。 |
| `poiID` | 字符串 | POI的唯一标识符。 |
| `type` | 字符串 | POI的常规类型，使用由POI定义的管理员选择的键入模式。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
