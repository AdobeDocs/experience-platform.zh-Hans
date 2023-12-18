---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；信标；交互详细信息；数据类型；数据类型；
solution: Experience Platform
title: 信标数据类型
description: 了解XDM Individual Profile类。
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 4%

---

# [!UICONTROL 信标] 数据类型

[!UICONTROL 信标] 是标准的XDM数据类型，描述在移动设备进入范围内时将身份信息传递给移动应用程序的无线设备。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `beaconMajor` | 双精度 | 主要值标识和区分1到65,535之间的一组无符号整数值。 |
| `beaconMinor` | 双精度 | 次要值标识和区分1到65,535之间的个别无符号整数值。 |
| `proximity` | 字符串 | 距信标的估计距离。 请参阅 [附录](#proximity) 以获取接受的值和定义。 |
| `proximityUUID` | 字符串 | 邻近UUID（通用唯一标识符）是一种特殊类型的标识符，用于将您的网络信标与非您控制网络中的所有其他信标区分开来。 邻近UUID被配置为信标，以发送到一定范围内的移动设备，以标识组织的信标。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## 附录

以下部分包含有关 [!UICONTROL 信标] 数据类型。

## 近似程度可接受的值 {#proximity}

下表概述了接受的值 `proximity` 以及它们的相关含义：

| 值 | 描述 |
| --- | --- |
| `immediate` | 几厘米以内。 |
| `near` | 离这里不到10米。 |
| `far` | 10米以外。 |
| `unknown` | 由于信号较弱，无法确定距离。 |
