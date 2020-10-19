---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;place context;placeContext;datatype;data-type;data type;
solution: Experience Platform
title: 放置上下文数据类型
topic: overview
description: 此文档概述了Place Context XDM数据类型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---


# [!UICONTROL 放置上下文] 数据类型

[!UICONTROL Place] context是一种标准XDM事件类型，用于描述观察到的数据的位置，包括兴趣点信息和地理坐标。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 兴趣点交互]](./poi-interaction.md) | 描述有关目标点(POI)交互的详细信息。 |
| `activePOIs` | 兴趣点 [[!UICONTROL 详细信息阵列]](./poi-details.md) | 描述导致事件的POI。 |
| `geo` | [[!UICONTROL 地域]](./geo.md) | 描述提供体验的地理位置。 |
| `localTime` | DateTime | RFC 3339格 [式的时间戳](https://tools.ietf.org/html/rfc3339) ，用指定的时区偏移指示本地时间。 格式模式 `yyyy-MM-dd'T'HH:mm:ssXXX` 为(例如 `2001-07-04T12:08:56-07:00`)。 |
| `localTimezoneOffset` | 整数 | 当前本地时区距UTC值的偏移(以分钟为单 `localTime` 位)。 这应包括当前DST偏移（如果适用）。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)