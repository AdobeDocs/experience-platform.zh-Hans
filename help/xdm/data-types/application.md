---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；应用程序；数据类型；数据类型；
solution: Experience Platform
title: 应用程序数据类型
description: 本文档概述了应用程序体验数据模型(XDM)数据类型。
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# [!UICONTROL 应用程序] 数据类型

[!UICONTROL 应用程序] 是一种标准的体验数据模型(XDM)数据类型，可描述与应用程序生成的交互相关的详细信息。 应用程序是指软件体验，如可由最终用户安装、运行、关闭或卸载的移动或桌面应用程序。 此数据类型的属性不用于描述聊天机器人、基于浏览器的插件或其他不适用于应用程序的体验等代理。

<img src="../images/data-types/application.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 测量]](./measure.md) | 描述有关终止应用程序的详细信息。 |
| `crashes` | [[!UICONTROL 测量]](./measure.md) | 当应用程序未按预期退出时，将触发此属性。 |
| `featureUsages` | [[!UICONTROL 测量]](./measure.md) | 描述所测量的应用程序功能激活过程中的任何数据。 |
| `firstLaunches` | [[!UICONTROL 测量]](./measure.md) | 包含首次启动时的数据。 此属性在安装后首次启动时触发。 |
| `installs` | [[!UICONTROL 测量]](./measure.md) | 当有特定安装事件可用时，记录设备上应用程序的安装。 |
| `launches` | [[!UICONTROL 测量]](./measure.md) | 描述与应用程序启动关联的值。 每次运行时都会触发该事件，包括崩溃次数、安装次数和在超出会话超时时从后台恢复次数。 |
| `upgrades` | [[!UICONTROL 测量]](./measure.md) | 包含有关升级之前已安装的应用程序的数据。 这会在升级后的首次启动时触发。 |
| `id` | 字符串 | 应用程序的唯一标识符。 |
| `name` | 字符串 | 应用程序的名称。 |
| `userPerspective` | 字符串 | 事件发生时用户与应用程序或品牌之间的视角或物理关系。 了解用户对应用程序的看法有助于在您不希望包含的大部分时间内准确地生成会话 `background` 和 `detached` 事件作为“活动”会话的一部分。 此属性的值必须等于下面列出的枚举值之一。 <li> `foreground`:用户和应用程序之间直接进行交互。 </li> <li> `background`:应用程序和用户之间是间接交互的。 例如，当屏幕被锁定或前台使用其他应用程序时，应用程序可能会测量一个值并刷新。  </li> <li> `detached`:“已分离”表示事件与应用程序相关，但并非直接从应用程序中发送，例如从外部系统发送电子邮件或推送通知。 |
| `version` | 字符串 | 应用程序的版本。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
