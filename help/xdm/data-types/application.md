---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；应用程序；数据类型；数据类型；
solution: Experience Platform
title: 应用程序数据类型
description: 本文档概述了Application Experience Data Model (XDM)数据类型。
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# [!UICONTROL 应用程序] 数据类型

[!UICONTROL 应用程序] 是一种标准的体验数据模型(XDM)数据类型，用于描述与应用程序生成的交互相关的详细信息。 应用程序是指软件体验，例如可由最终用户安装、运行、关闭或卸载的移动或桌面应用程序。 此数据类型的属性并非用于描述代理，例如聊天机器人、基于浏览器的插件或其他不适用于应用程序的体验。

<img src="../images/data-types/application.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 衡量]](./measure.md) | 描述有关应用程序终止的详细信息。 |
| `crashes` | [[!UICONTROL 衡量]](./measure.md) | 当应用程序未按预期退出时，将触发此属性。 |
| `featureUsages` | [[!UICONTROL 衡量]](./measure.md) | 描述激活正在测量的应用程序功能所产生的任何数据。 |
| `firstLaunches` | [[!UICONTROL 衡量]](./measure.md) | 包含有关首次启动的数据。 此属性在安装后首次启动时触发。 |
| `installs` | [[!UICONTROL 衡量]](./measure.md) | 在特定安装事件可用时，记录应用程序在设备上的安装。 |
| `launches` | [[!UICONTROL 衡量]](./measure.md) | 描述与应用程序启动关联的值。 每次运行时，都会触发此事件，包括崩溃、安装，以及在超出会话超时后从后台恢复。 |
| `upgrades` | [[!UICONTROL 衡量]](./measure.md) | 包含有关升级之前已安装的应用程序的数据。 这会在升级后的首次启动时触发。 |
| `id` | 字符串 | 应用程序的唯一标识符。 |
| `name` | 字符串 | 应用程序的名称。 |
| `userPerspective` | 字符串 | 发生事件时用户和应用程序或品牌之间的透视关系或实体关系。 了解用户相对于应用程序的视角，有助于在大部分情况下准确地生成会话，因为您不希望将会话包含在内 `background` 和 `detached` 作为“活动”会话一部分的事件。 此属性的值必须等于下面列出的枚举值之一。 <li> `foreground`：用户和应用程序正在直接彼此交互。 </li> <li> `background`：应用程序和用户正在间接彼此进行交互。 例如，应用程序可以测量值，并在屏幕锁定或前台使用其他应用程序时刷新。  </li> <li> `detached`：分离是指该事件与应用程序相关，但并非直接来自应用程序，例如从外部系统发送电子邮件或推送通知。 |
| `version` | 字符串 | 应用程序的版本。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
