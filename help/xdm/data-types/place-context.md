---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；放置上下文；placeContext；数据类型；数据类型；
solution: Experience Platform
title: 放置上下文数据类型
description: 本文档概述了“置入上下文XDM”数据类型。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---

# [!UICONTROL 放置上下文] 数据类型

[!UICONTROL 放置上下文] 是一种标准的XDM数据类型，用于描述观察到的事件的位置，包括目标点信息和地理坐标。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 目标点互动]](./poi-interaction.md) | 描述有关目标点(POI)交互的详细信息。 |
| `activePOIs` | 数组 [[!UICONTROL 目标点详细信息]](./poi-details.md) | 描述导致事件的POI。 |
| `geo` | [[!UICONTROL 地域]](./geo.md) | 描述体验交付的地理位置。 |
| `localTime` | DateTime | 中的时间戳 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式，指示使用的具有规定时区偏移的本地时间。 格式模式为 `yyyy-MM-dd'T'HH:mm:ssXXX` (例如， `2001-07-04T12:08:56-07:00`)。 |
| `localTimezoneOffset` | 整数 | 当前本地时区与UTC的偏移（以分钟为单位） `localTime` 值。 这应包括当前夏令时偏移（如果适用）。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
