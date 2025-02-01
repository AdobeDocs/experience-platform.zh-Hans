---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；POI；交互；兴趣点；兴趣点；数据类型；数据类型；
solution: Experience Platform
title: 兴趣点交互数据类型
description: 了解兴趣点交互XDM数据类型。
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL 兴趣点交互]数据类型

[!UICONTROL 兴趣点交互]是一种标准XDM数据类型，它描述了在移动设备进入范围内时将身份信息传递给移动应用程序的无线设备。

![](../images/data-types/poi-interaction.png){width=400}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 兴趣点详细信息]](./poi-details.md) | 描述导致事件的POI的详细信息。 |
| `poiEntries` | 对象 | 描述人员进入POI的次数。 包含两个属性： <ul><li>`id`：度量值的唯一标识符。</li><li>`value`：度量值的可量化值。</li></ul> |
| `poiExits` | 对象 | 描述人员退出POI的次数。 包含两个属性： <ul><li>`id`：度量值的唯一标识符。</li><li>`value`：度量值的可量化值。</li></ul> |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
