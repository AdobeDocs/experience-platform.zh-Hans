---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；信标；交互详细信息；数据类型；数据类型；
solution: Experience Platform
title: 信标数据类型
topic-legacy: overview
description: 本文档概述了XDM单个用户档案类。
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 3%

---

# [!UICONTROL Beacon] 数据类型

[!UICONTROL Beacon] 是一种标准的XDM数据类型，用于描述当移动设备在范围内时向移动应用程序传送身份信息的无线设备。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `beaconMajor` | 双精度 | 主值标识和区分1到65,535之间的组和无符号整数值。 |
| `beaconMinor` | 双精度 | 次值标识和区分介于1和65,535之间的单个和无符号整数值。 |
| `proximity` | 字符串 | 估计距离信标。 有关已接受的值和定义，请参见[附录](#proximity)。 |
| `proximityUUID` | 字符串 | 近似UUID（通用唯一标识符）是一种特殊类型的标识符，用于区分网络中的信标和您控制之外的网络中的所有其他信标。 邻近UUID被配置成信标，被传输到范围内的移动设备以标识组织的信标。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## 附录

以下部分包含有关[!UICONTROL Beacon]数据类型的其他信息。

## 接近{#proximity}的已接受值

下表概述了`proximity`的已接受值及其相关含义：

| 值 | 描述 |
| --- | --- |
| `immediate` | 几厘米内。 |
| `near` | 不到10米。 |
| `far` | 距离酒店超过10米。 |
| `unknown` | 由于信号弱，距离无法确定。 |
