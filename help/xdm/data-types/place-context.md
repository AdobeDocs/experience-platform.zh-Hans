---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；置入上下文；placeContext;datatype；数据类型；
solution: Experience Platform
title: 置入上下文数据类型
topic-legacy: overview
description: 本文档概述了Place Context XDM数据类型。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 4%

---

# [!UICONTROL Place context] 数据类型

[!UICONTROL Place context] 是一种标准的XDM事件类型，用于描述观察到的数据的位置，包括目标点信息和地理坐标。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | 描述有关目标点(POI)交互的详细信息。 |
| `activePOIs` | [[!UICONTROL Point of interest details]](./poi-details.md)的数组 | 描述导致事件的POI。 |
| `geo` | [[!UICONTROL Geo]](./geo.md) | 描述提供体验的地理位置。 |
| `localTime` | DateTime | 以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式的时间戳，指示使用的本地时间与规定的时区偏移。 格式设置模式为`yyyy-MM-dd'T'HH:mm:ssXXX`（例如`2001-07-04T12:08:56-07:00`）。 |
| `localTimezoneOffset` | 整数 | 当前本地时区偏移（以分钟为单位）与`localTime`值的UTC之间的偏移。 这应包括当前DST偏移（如果适用）。 |

有关混音的更多详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
