---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；浏览器；浏览器详细信息；数据类型；数据类型；
solution: Experience Platform
title: 浏览器详细信息数据类型
topic: overview
description: 此文档概述了浏览器详细信息XDM数据类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 6%

---


# [!UICONTROL 浏览器详] 细信息数据类型

[!UICONTROL 浏览] 器详细信息是一种标准XDM数据类型，它描述与浏览器或应用程序相关的详细信息。

<img src="../images/data-types/browser-details.png" width="450" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `acceptLanguage` | 字符串 | IETF语言标签([RFC 5646](https://tools.ietf.org/html/rfc5646))。 |
| `cookiesEnabled` | 布尔值 | 指示用户的设置是否允许写入Cookie。 |
| `javaEnabled` | 布尔值 | 指示设备中是否启用了Java，这是从中进行观察的。 |
| `javaScriptEnabled` | 布尔值 | 指示是否在观察所基于的设备中启用了JavaScript。 |
| `javaScriptVersion` | 字符串 | 在观察过程中支持的JavaScript版本。 |
| `javaVersion` | 字符串 | 在观察过程中支持的Java版本。 |
| `name` | 字符串 | 应用程序或浏览器名称。 |
| `quicktimeVersion` | 字符串 | 在观察期间支持的Apple Quicktime版本。 |
| `thirdPartyCookiesEnabled` | 布尔值 | 指示是否在进行观察的设备中启用了第三方Cookie。 |
| `userAgent` | 字符串 | 客户端请求中的HTTP用户代理字符串。 |
| `vendor` | 字符串 | 应用程序或浏览器供应商。 |
| `version` | 字符串 | 应用程序或浏览器版本。 |
| `viewportHeight` | 整数 | 窗口内显示事件的垂直大小（以像素为单位）。 对于Web视图事件，这是浏览器视口高度。 |
| `viewportWidth` | 整数 | 窗口内显示事件的水平大小（以像素为单位）。 对于Web视图事件，这是浏览器视图端口宽度。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)