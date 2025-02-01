---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；环境；数据类型；数据类型；
solution: Experience Platform
title: 环境数据类型
description: 了解环境XDM数据类型。
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 12%

---

# [!UICONTROL 环境]数据类型

[!UICONTROL 环境]是一种标准XDM数据类型，它描述了观察到的事件的周围环境，特别是详细说明网络和软件版本等临时信息。

>[!IMPORTANT]
>
>所有值都应与[DeviceAtlas](https://deviceatlas.com)数据库保持一致，并由Adobe授予许可。

![](../images/data-types/environment.png){width=400}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_dc` | 对象 | 包含单个字段`language`的对象，该字段指示用于表示用户对数据表示的语言、地理或文化偏好设置的环境语言。 在[IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt)中定义的语言代码中指定语言。 |
| `browserDetails` | [浏览器详细信息](./browser-details.md) | 描述环境的特定于浏览器的详细信息，如浏览器名称、版本、JavaScript版本、用户代理字符串和接受语言。 |
| `ISP` | 字符串 | 用户的 Internet 服务提供商的名称。 |
| `carrier` | 字符串 | 向用户销售和交付通信服务的移动网络运营商或MNO（也称为无线服务提供商、无线运营商、蜂窝公司或移动网络运营商）的名称。 |
| `colorDepth` | 整数 | 用于单个像素的每个颜色分量的位数。 |
| `connectionType` | 字符串 | Internet连接类型。 接受的值包括： <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 字符串 | 用户ISP的域。 |
| `ipV4` | 字符串 | 分配给参与使用Internet协议进行通信（32位）的计算机网络的设备的数字标签。 |
| `ipV6` | 字符串 | 分配给参与使用Internet协议进行通信（128位）的计算机网络的设备的数字标签。 |
| `operatingSystem` | 字符串 | 进行观察时使用的操作系统的名称。 该属性不应包含任何版本信息，如`10.5.3`，而应包含“版本”标注，如`Ultimate`或`Professional`。 |
| `operatingSystemVendor` | 字符串 | 进行观察时使用的操作系统供应商的名称。 |
| `operatingSystemVersion` | 字符串 | 进行观察时使用的操作系统的完整版本标识符。 版本通常由数字组成，但可以采用供应商定义的格式。 |
| `type` | 字符串 | 应用程序环境的类型。 请参阅[附录](#type)以了解接受的值。 |
| `viewportHeight` | 整数 | 显示体验的窗口的垂直大小（像素）。 对于Web视图事件，这是浏览器视区高度。 |
| `viewPortWidth` | 整数 | 显示体验的窗口的水平大小（像素）。 对于Web视图事件，这是浏览器视区宽度。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 附录

以下部分包含有关[!UICONTROL 设备]数据类型的其他信息。

## 类型的接受值 {#type}

下表概述了`type`的接受值及其相关含义：

| 值 | 描述 |
| --- | --- |
| `browser` | 浏览器 |
| `application` | 应用程序 |
| `iot` | 物联网 |
| `external` | 外部系统 |
| `widget` | 应用程序扩展 |
