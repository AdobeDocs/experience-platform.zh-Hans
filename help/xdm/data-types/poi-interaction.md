---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；poi；交互；目标点；目标点；数据类型；数据类型；
solution: Experience Platform
title: 兴趣点交互数据类型
description: 本文档概述了兴趣点交互XDM数据类型。
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 3%

---

# [!UICONTROL 目标点互动] 数据类型

[!UICONTROL 目标点互动] 是一种标准的XDM数据类型，用于描述在移动设备处于范围内时向移动设备应用程序传递身份信息的无线设备。

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 目标点详细信息]](./poi-details.md) | 描述导致事件的POI的详细信息。 |
| `poiEntries` | 对象 | 描述人员进入POI的次数。 包含两个属性： <ul><li>`id`:度量的唯一标识符。</li><li>`value`:量度的可量化值。</li></ul> |
| `poiExits` | 对象 | 描述人员退出POI的次数。 包含两个属性： <ul><li>`id`:度量的唯一标识符。</li><li>`value`:量度的可量化值。</li></ul> |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
