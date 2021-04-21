---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;poi；交互；目标点；目标点；数据类型；数据类型；
solution: Experience Platform
title: 兴趣点交互数据类型
topic-legacy: overview
description: 本文档概述了兴趣点交互XDM数据类型。
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# [!UICONTROL Point of interest interaction] 数据类型

[!UICONTROL Point of interest interaction] 是一种标准的XDM数据类型，用于描述当移动设备在范围内时向移动应用程序传送身份信息的无线设备。

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | 描述导致事件的POI的详细信息。 |
| `poiEntries` | 对象 | 描述个人输入POI的次数。 包含两个属性： <ul><li>`id`:度量的唯一标识符。</li><li>`value`:量度的可量化价值。</li></ul> |
| `poiExits` | 对象 | 描述人员退出POI的次数。 包含两个属性： <ul><li>`id`:度量的唯一标识符。</li><li>`value`:量度的可量化价值。</li></ul> |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
