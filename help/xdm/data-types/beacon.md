---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；信标；交互详细信息；数据类型；数据类型；
solution: Experience Platform
title: 信标数据类型
description: 本文档概述了XDM Individual Profile类。
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 4%

---

# [!UICONTROL 信标] 数据类型

[!UICONTROL 信标] 是一种标准的XDM数据类型，用于描述在移动设备处于范围内时向移动设备应用程序传递身份信息的无线设备。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `beaconMajor` | 双精度 | 主要值标识和区分1到65,535之间的组和无符号整数值。 |
| `beaconMinor` | 双精度 | 次要值标识和区分1到65,535之间的单个和无符号整数值。 |
| `proximity` | 字符串 | 估计与信标的距离。 请参阅 [附录](#proximity) 以了解接受的值和定义。 |
| `proximityUUID` | 字符串 | 邻近UUID（通用唯一标识符）是一种特殊类型的标识符，用于将网络中的信标与您控制之外的网络中的所有其他信标区分开来。 邻近UUID被配置为信标，以传输到范围内的移动设备，以标识组织的信标。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## 附录

以下部分包含有关 [!UICONTROL 信标] 数据类型。

## 接近度的接受值 {#proximity}

下表概述了 `proximity` 及其相关含义：

| 值 | 描述 |
| --- | --- |
| `immediate` | 几厘米之内。 |
| `near` | 不到10米。 |
| `far` | 距离酒店10米以上。 |
| `unknown` | 由于信号微弱，无法确定距离。 |
