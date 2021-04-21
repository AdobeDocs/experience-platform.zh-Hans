---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；度量；数据类型；数据类型；
solution: Experience Platform
title: 度量数据类型
topic-legacy: overview
description: 本文档概述了测量体验数据模型(XDM)数据类型。
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 1%

---

# [!UICONTROL Measure] 数据类型

[!UICONTROL Measure] 是标准的体验数据模型(XDM)数据类型，包含特定量度的具体可量化数据点。度量由唯一标识符和值组成。

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `id` | 字符串 | 此度量的唯一标识符。 如果使用有损通信渠道（例如具有脱机功能的移动应用程序或网站）进行数据收集，则无法确保测量的传输，则此属性包含客户端生成的所采取测量的唯一ID。 最好让这种情况足够长，以确保足够的随机性。 <br><br> 如果在生成时包含时间戳、设备ID、IP、MAC地址或其他潜在用户识别值等信息，则 `id`结果应进行散列处理。这可以确保不在值中对PII进行编码，因为目标不是识别用户或设备，而是识别特定的时间度量。 |
| `value` | 双精度 | 这个量度的可量化价值。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
