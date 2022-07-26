---
title: 广告时间数据类型
description: 本文档概述了广告时间体验数据模型(XDM)数据类型。
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 6%

---

# [!UICONTROL 广告时间] 数据类型

[!UICONTROL 广告时间] 是一种标准的体验数据模型(XDM)数据类型，用于描述如何将定时广告插入到定时媒体中。

![数据类型结构](../images/data-types/ad-break.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_dc.title` | 字符串 | 广告时间的易记名称。 |
| `_id` | 字符串 | 广告时间的唯一标识符。 |
| `offset` | 整数 | 广告时间与主内容开始的偏移，以秒为单位。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
