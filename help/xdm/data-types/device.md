---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；设备；数据类型；数据类型；
solution: Experience Platform
title: 设备数据类型
topic: overview
description: 此文档概述了设备XDM数据类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 4%

---


# [!UICONTROL 设] 备数据类型

[!UICONTROL 设] 备是描述已识别设备的标准XDM数据类型。设备是可跨会话跟踪的应用程序或浏览器实例，通常由cookie跟踪。

<img src="../images/data-types/device.png" width="450" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `colorDepth` | 整数 | 显示屏能够表示的颜色数。 |
| `manufacturer` | 字符串 | 设备设计和创建的所有组织的名称。 |
| `model` | 字符串 | 设备的型号名称。 这是设备的通用、可读或营销名称。 例如，“iPhone 6S”是手机的特定型号。 |
| `modelNumber` | 字符串 | 制造商为此设备分配的唯一型号指定。 型号不是版本，而是标识特定型号配置的唯一标识符。 |
| `screenHeight` | 整数 | 设备在默认方向上的活动显示的垂直像素数。 |
| `screenOrientation` | 字符串 | 当前屏幕方向。 接受的值包括`portrait`和`landscape`。 |
| `screenWidth` | 字符串 | 设备在默认方向上的活动显示的水平像素数。 |
| `type` | 字符串 | 要跟踪的设备类型。 接受的值包括： <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | 字符串 | 设备的标识符。 这可以是DeviceAtlas的标识符或标识正在使用的硬件的其他服务。 |
| `typeIDService` | 字符串 | 用于标识设备类型的服务的命名空间。 有关已接受值的详细信息，请参见[附录](#typeIDService)。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## 附录

以下部分包含有关[!UICONTROL Device]数据类型的其他信息。

## typeIDService {#typeIDService}已接受值

下表概述了`typeIDService`的已接受值及其相关含义：

| 值 | 描述 |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | 设备已使用DeviceAtlas进行识别。 |
| `https://ns.adobe.com/xdm/external/adobecampaign` | 已使用Adobe Campaign识别设备。 |