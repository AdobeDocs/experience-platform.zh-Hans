---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；测量；数据类型；数据类型；
solution: Experience Platform
title: 度量数据类型
description: 本文档概述了Measure Experience Data Model (XDM)数据类型。
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---

# [!UICONTROL 衡量] 数据类型

[!UICONTROL 衡量] 是一种标准体验数据模型(XDM)数据类型，包含特定量度的具体可量化数据点。 度量值由唯一标识符和值组成。

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `id` | 字符串 | 此度量的唯一标识符。 在使用有损通信渠道（如无法确保传输测量结果的移动应用程序或具有离线功能的网站）收集数据时，此属性包含由客户端生成的测量结果的唯一ID。 最佳实践是使时间足够长以确保足够的随机性。 <br><br> 如果时间戳、设备ID、IP、MAC地址或其他可能的用户标识值等信息被纳入到生成的 `id`，则结果应进行哈希处理。 这可以确保值中不对PII进行编码，因为目标不是识别用户或设备，而是及时识别特定的衡量标准。 |
| `value` | 双精度 | 此衡量标准的可量化值。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
