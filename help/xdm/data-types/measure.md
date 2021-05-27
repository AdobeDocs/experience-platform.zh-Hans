---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；测量；数据类型；数据类型；
solution: Experience Platform
title: 测量数据类型
topic-legacy: overview
description: 本文档概述了测量体验数据模型(XDM)数据类型。
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

#  测量数据类型

 测量是一种标准的体验数据模型(XDM)数据类型，其中包含特定量度的可量化具体数据点。度量由唯一标识符和值组成。

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `id` | 字符串 | 此度量的唯一标识符。 如果使用有损通信渠道（如具有离线功能的移动应用程序或网站）收集数据，但无法确保测量的传输，则此属性包含由客户端生成且所采用测量的唯一ID。 最好的做法是，让这一时间足够长，以确保足够的随机性。 <br><br> 如果在生成时包含时间戳、设备ID、IP、MAC地址或其他潜在用户标识值等信息，则 `id`结果应经过哈希处理。这可确保值中不会对PII进行编码，因为其目标不是识别用户或设备，而是及时显示特定的度量。 |
| `value` | 双精度 | 此度量的可量化值。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
