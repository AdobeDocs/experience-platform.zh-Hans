---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；POI；POI详细信息；目标点；目标点详细信息；数据类型；数据类型；
solution: Experience Platform
title: 兴趣点详细信息数据类型
description: 了解兴趣点详细信息XDM数据类型。
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 15%

---

# [!UICONTROL 兴趣点详细信息]数据类型

[!UICONTROL 兴趣点详细信息]是一个标准XDM数据类型，用于描述观察到事件的地理相关数据。

![](../images/data-types/poi-details.png){width=550}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL 信标]](./beacon.md) | 描述适用于POI交互的信标详细信息。 |
| `geoInteractionDetails` | [[!UICONTROL 地理位置交互详细信息]](./geo-interaction-details.md) | 描述适用于POI交互的地理详细信息。 |
| `category` | 字符串 | 由POI定义管理员分配的用于组织POI的一般类别。 |
| `distanceToPOICenter` | 双精度 | 与POI中心的估计距离（以米为单位）。 |
| `locatingType` | 字符串 | 用于确定位置的机制。 接受的值包括： <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 字符串 | 为POI指定的名称。 |
| `poiID` | 字符串 | POI的唯一标识符。 |
| `type` | 字符串 | 使用 POI 定义管理员选择的键入架构的 POI 的一般类型。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
