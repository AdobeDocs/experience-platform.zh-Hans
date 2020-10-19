---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;interaction;point of interest;point-of-interest;datatype;data-type;data type;
solution: Experience Platform
title: 兴趣点交互数据类型
topic: overview
description: 此文档概述了兴趣点交互XDM数据类型。
translation-type: tm+mt
source-git-commit: 032adc72db7f094b268f14e8f7d48810830a84e4
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---


# [!UICONTROL 兴趣点交互] 数据类型

[!UICONTROL 兴趣点交互] 是一种标准XDM数据类型，描述在移动设备处于范围内时向移动应用程序传送身份信息的无线设备。

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 兴趣点详细信息]](./poi-details.md) | 描述导致事件的POI的详细信息。 |
| `poiEntries` | 对象 | 描述人员输入POI的次数。 包含两个属性： <ul><li>`id`:度量的唯一标识符。</li><li>`value`:度量的可量化价值。</li></ul> |
| `poiExits` | 对象 | 描述人员退出POI的次数。 包含两个属性： <ul><li>`id`:度量的唯一标识符。</li><li>`value`:度量的可量化价值。</li></ul> |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
