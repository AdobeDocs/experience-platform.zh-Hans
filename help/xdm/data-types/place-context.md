---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；位置上下文；placeContext；数据类型；数据类型；
solution: Experience Platform
title: 地标上下文数据类型
description: 了解位置上下文XDM数据类型。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# [!UICONTROL 放置上下文]数据类型

[!UICONTROL 放置上下文]是一个标准XDM数据类型，它描述了观察到的事件的位置，包括兴趣点信息和地理坐标。

![](../images/data-types/place-context.png){width=500}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 兴趣点互动]](./poi-interaction.md) | 描述有关兴趣点(POI)交互的详细信息。 |
| `activePOIs` | [[!UICONTROL 目标点详细信息]](./poi-details.md)的数组 | 描述导致事件的POI。 |
| `geo` | [[!UICONTROL 地域]](./geo.md) | 描述提供体验的地理位置。 |
| `localTime` | 日期时间 | 以[RFC 3339](https://tools.ietf.org/html/rfc3339)格式表示的时间戳，指示使用具有规定时区偏移量的本地时间。 格式模式为`yyyy-MM-dd'T'HH:mm:ssXXX`（例如，`2001-07-04T12:08:56-07:00`）。 |
| `localTimezoneOffset` | 整数 | `localTime`值的当前本地时区与UTC的偏移量（以分钟为单位）。 这应包括当前DST偏移（如果适用）。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
