---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；应用程序；数据类型；数据类型；
solution: Experience Platform
title: 应用程序数据类型
description: 了解应用程序体验数据模型(XDM)数据类型。
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 1%

---

# [!UICONTROL 应用程序]数据类型

[!UICONTROL 应用程序]是一种标准的体验数据模型(XDM)数据类型，它描述了与应用程序生成的交互相关的详细信息。 应用程序是指软件体验，例如可由最终用户安装、运行、关闭或卸载的移动或桌面应用程序。 此数据类型的属性并非旨在描述代理，例如聊天机器人、基于浏览器的插件或其他不适用于应用程序的体验。

![应用程序图像](../images/data-types/application.PNG){width=500}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 度量值]](./measure.md) | 描述有关应用程序终止的详细信息。 |
| `crashes` | [[!UICONTROL 度量值]](./measure.md) | 当应用程序未按预期退出时，将触发此属性。 |
| `featureUsages` | [[!UICONTROL 度量值]](./measure.md) | 描述激活正在测量的应用程序功能所产生的任何数据。 |
| `firstLaunches` | [[!UICONTROL 度量值]](./measure.md) | 包含有关首次启动的数据。 此属性在安装后首次启动时触发。 |
| `installs` | [[!UICONTROL 度量值]](./measure.md) | 在特定安装事件可用时，记录应用程序在设备上的安装。 |
| `launches` | [[!UICONTROL 度量值]](./measure.md) | 描述与应用程序启动关联的值。 在每次运行时都会触发此事件，包括崩溃、安装以及在超出会话超时后从后台恢复。 |
| `upgrades` | [[!UICONTROL 度量值]](./measure.md) | 包含有关升级之前已安装的应用程序的数据。 这会在升级后的首次启动时触发。 |
| `id` | 字符串 | 应用程序的唯一标识符。 |
| `name` | 字符串 | 应用程序的名称。 |
| `userPerspective` | 字符串 | 事件发生时用户和应用程序或品牌之间的视角或物理关系。 了解用户相对于应用程序的角度有助于准确生成会话，因为大多数情况下，您不希望将`background`和`detached`事件包含在“活动”会话中。 此属性的值必须等于下面列出的枚举值之一。 <li> `foreground`：用户和应用程序正在相互直接交互。 </li> <li> `background`：应用程序和用户正在间接交互操作。 例如，应用程序可以测量值，并在屏幕锁定或前台使用其他应用程序时刷新。  </li> <li> `detached`： Detached表示该事件与应用程序相关，但并非直接来自应用程序，例如从外部系统发送电子邮件或推送通知。 |
| `version` | 字符串 | 应用程序的版本。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
