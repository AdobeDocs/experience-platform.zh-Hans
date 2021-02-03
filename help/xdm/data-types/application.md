---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；应用程序；数据类型；数据类型；
solution: Experience Platform
title: 应用程序数据类型
topic: overview
description: 本文档概述了应用程序体验数据模型(XDM)数据类型。
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---


# [!UICONTROL 应] 用程序数据类型

[!UICONTROL 应用] 程序是一种标准的体验数据模型(XDM)数据类型，它描述与应用程序生成的交互相关的详细信息。应用程序是指软件体验，如可由最终用户安装、运行、关闭或卸载的移动或桌面应用程序。 此数据类型的属性不用于描述聊天机器人、基于浏览器的插件或其他不适用于应用程序的体验等代理。

<img src="../images/data-types/application.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 度量]](./measure.md) | 描述有关应用程序终止的详细信息。 |
| `crashes` | [[!UICONTROL 度量]](./measure.md) | 当应用程序未按预期退出时，此属性将触发。 |
| `featureUsages` | [[!UICONTROL 度量]](./measure.md) | 描述所测量的应用程序功能激活中的任何数据。 |
| `firstLaunches` | [[!UICONTROL 度量]](./measure.md) | 包含首次启动时的数据。 此属性在安装后首次启动时触发。 |
| `installs` | [[!UICONTROL 度量]](./measure.md) | 当特定安装事件可用时，在设备上记录应用程序的安装。 |
| `launches` | [[!UICONTROL 度量]](./measure.md) | 描述与应用程序启动关联的值。 每次运行时都会触发该错误，包括崩溃、安装和从后台恢复（当超出会话超时时）。 |
| `upgrades` | [[!UICONTROL 度量]](./measure.md) | 包含有关之前已安装的应用程序升级的数据。 升级后首次启动时将触发此信息。 |
| `id` | 字符串 | 应用程序的唯一标识符。 |
| `name` | 字符串 | 应用程序的名称。 |
| `userPerspective` | 字符串 | 事件发生时用户与应用程序或品牌之间的透视或物理关系。 了解用户对应用程序的看法有助于准确地生成会话，因为大多数时间您不希望将`background`和`detached`事件作为“活动”会话的一部分。 此属性的值必须等于下面列出的枚举值之一。 <li> `foreground`:用户和应用程序之间直接进行交互。 </li> <li> `background`:应用和用户间接互动。例如，应用程序可以测量值并在屏幕被锁定或前景中使用其他应用程序时刷新。  </li> <li> `detached`:分离表示事件与应用程序相关，但不直接来自应用程序，如从外部系统发送电子邮件或推送通知。 |
| `version` | 字符串 | 应用程序的版本。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)