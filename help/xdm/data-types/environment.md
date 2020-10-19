---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;environment;datatype;data-type;data type;
solution: Experience Platform
title: 环境数据类型
topic: overview
description: 此文档概述了环境XDM数据类型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 4%

---


# [!UICONTROL 环境] 数据类型

[!UICONTROL 环境] 是一种标准的XDM环境类型，它描述观察到的事件的周围，特别详细描述诸如网络和软件版本等暂时性信息。

>[!IMPORTANT]
>
>所有值应与DeviceAtlas数据 [库一致](https://deviceatlas.com) ，由Adobe授权。

<img src="../images/data-types/environment.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_dc` | 对象 | 包含单个字段的对象， `language`该字段指示环境的语言，以表示用户的语言、地理或文化偏好来表示数据演示。 语言在IETF RFC 3066中定义的语 [言代码中指定](https://www.ietf.org/rfc/rfc3066.txt)。 |
| `browserDetails` | [浏览器详细信息](./browser-details.md) | 描述浏览器特定的环境详细信息，如浏览器名称、版本、JavaScript版本、用户代理字符串和接受语言。 |
| `ISP` | 字符串 | 用户的Internet服务提供商的名称。 |
| `carrier` | 字符串 | 向用户销售和提供通信服务的移动网络运营商或MNO(也称为无线服务提供商、无线运营商、蜂窝公司或移动网络运营商)的名称。 |
| `colorDepth` | 整数 | 用于单个像素的每个颜色分量的位数。 |
| `connectionType` | 字符串 | Internet连接类型。 接受的值包括： <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 字符串 | 用户ISP的域。 |
| `ipV4` | 字符串 | 指定给参与使用因特网协议进行通信（32位）的计算机网络的设备的数字标签。 |
| `ipV6` | 字符串 | 指定给参与使用因特网协议进行通信（128位）的计算机网络的设备的数字标签。 |
| `operatingSystem` | 字符串 | 进行观察时使用的操作系统的名称。 属性不应包含任何版本信息(如 `10.5.3`)，而应包含“版本”名称(如 `Ultimate` 或) `Professional`。 |
| `operatingSystemVendor` | 字符串 | 进行观察时使用的操作系统供应商的名称。 |
| `operatingSystemVersion` | 字符串 | 进行观察时所使用的操作系统的完整版本标识符。 版本通常由数字组成，但可采用供应商定义的格式。 |
| `type` | 字符串 | 应用程序环境的类型。 有关已接受 [的值](#type) ，请参阅附录。 |
| `viewportHeight` | 整数 | 体验显示在窗口内的垂直大小（以像素为单位）。 对于Web视图事件，这是浏览器视口高度。 |
| `viewPortWidth` | 整数 | 体验显示在其中的窗口的水平大小（以像素为单位）。 对于Web视图事件，这是浏览器视图端口宽度。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 附录

以下部分包含有关设备数据类 [!UICONTROL 型的] 其他信息。

## 已接受类型值 {#type}

下表概述了可接受的值及其 `type` 相关含义：

| 值 | 描述 |
| --- | --- |
| `browser` | 浏览器 |
| `application` | 应用程序 |
| `iot` | 物联网 |
| `external` | 外部系统 |
| `widget` | 应用程序扩展 |