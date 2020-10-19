---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: 信标数据类型
topic: overview
description: 此文档概述了XDM单个用户档案类。
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---


# [!UICONTROL 信标] 数据类型

[!UICONTROL 信标] 是标准XDM数据类型，用于描述当移动设备在范围内时向移动应用程序传送身份信息的无线设备。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `beaconMajor` | 双精度 | 主要值标识和区分1到65,535之间的组和无符号整数值。 |
| `beaconMinor` | 双精度 | 次要值标识和区分介于1和65,535之间的单个和无符号整数值。 |
| `proximity` | 字符串 | 估计与信标的距离。 有关已接 [受的值](#proximity) 和定义，请参阅附录。 |
| `proximityUUID` | 字符串 | 邻近UUID(Unerally Unique Identifier)是一种特殊类型的标识符，用于区分网络中的信标和控制外网络中的所有其他信标。 邻近UUID被配置成信标，被传输到范围内的移动设备以标识组织的信标。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## 附录

以下部分包含有关信标数据类 [!UICONTROL 型的] 其他信息。

## 接近度的已接受值 {#proximity}

下表概述了可接受的值及其 `proximity` 相关含义：

| 值 | 描述 |
| --- | --- |
| `immediate` | 几厘米内。 |
| `near` | 不到10米外。 |
| `far` | 距离酒店超过10米。 |
| `unknown` | 距离无法确定，可能是由于信号弱。 |