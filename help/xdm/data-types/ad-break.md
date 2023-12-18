---
title: 广告时间数据类型
description: 了解广告时间体验数据模型(XDM)数据类型。
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 6%

---

# [!UICONTROL 广告时间] 数据类型

[!UICONTROL 广告时间] 是一种标准的体验数据模型(XDM)数据类型，描述如何将定时广告插入定时媒体中。

![数据类型结构](../images/data-types/ad-break.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_dc.title` | 字符串 | 广告时间的友好名称。 |
| `_id` | 字符串 | 广告时间的唯一标识符。 |
| `offset` | 整数 | 广告时间从主要内容开始的偏移，以秒为单位。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
