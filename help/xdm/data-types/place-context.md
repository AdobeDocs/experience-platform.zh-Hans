---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；置入上下文；placeContext;datatype；数据类型；
solution: Experience Platform
title: 放置上下文数据类型
topic: overview
description: 此文档概述了Place Context XDM数据类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---


# [!UICONTROL 放置] 上下文数据类型

[!UICONTROL 放置] 上下文是一种标准XDM数据类型，用于描述观察事件的位置，包括兴趣点信息和地理坐标。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 兴趣点交互]](./poi-interaction.md) | 描述有关目标点(POI)交互的详细信息。 |
| `activePOIs` | [[!UICONTROL 兴趣点详细信息]](./poi-details.md)的数组 | 描述导致事件的POI。 |
| `geo` | [[!UICONTROL 地域]](./geo.md) | 描述提供体验的地理位置。 |
| `localTime` | DateTime | 以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式的时间戳，用规定的时区偏移指示本地时间。 格式模式为`yyyy-MM-dd'T'HH:mm:ssXXX`（例如`2001-07-04T12:08:56-07:00`）。 |
| `localTimezoneOffset` | 整数 | 当前本地时区偏移（以分钟为单位）与`localTime`值的UTC之间的偏移。 这应包括当前DST偏移（如果适用）。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)