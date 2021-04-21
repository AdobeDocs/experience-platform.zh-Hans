---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；应用程序；数据类型；数据类型；
solution: Experience Platform
title: 应用程序数据类型
topic-legacy: overview
description: 本文档概述了应用程序体验数据模型(XDM)数据类型。
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 1%

---

# [!UICONTROL Application] 数据类型

[!UICONTROL Application] 是标准的体验数据模型(XDM)数据类型，它描述与应用程序生成的交互相关的详细信息。应用程序是指软件体验，如可由最终用户安装、运行、关闭或卸载的移动或桌面应用程序。 此数据类型的属性不用于描述代理，如聊天机器人、基于浏览器的插件或不适用于应用程序的其他体验。

<img src="../images/data-types/application.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Measure]](./measure.md) | 介绍有关应用程序终止的详细信息。 |
| `crashes` | [[!UICONTROL Measure]](./measure.md) | 当应用程序未按预期退出时，会触发此属性。 |
| `featureUsages` | [[!UICONTROL Measure]](./measure.md) | 描述所测量的应用程序功能激活中的任何数据。 |
| `firstLaunches` | [[!UICONTROL Measure]](./measure.md) | 包含首次启动时的数据。 此属性在安装后首次启动时触发。 |
| `installs` | [[!UICONTROL Measure]](./measure.md) | 当特定安装事件可用时，在设备上记录应用程序的安装。 |
| `launches` | [[!UICONTROL Measure]](./measure.md) | 描述与应用程序启动关联的值。 每次运行都会触发该事件，包括超出会话超时时的崩溃、安装和从后台恢复。 |
| `upgrades` | [[!UICONTROL Measure]](./measure.md) | 包含有关之前已安装的应用程序升级的数据。 这是在升级后首次启动时触发的。 |
| `id` | 字符串 | 应用程序的唯一标识符。 |
| `name` | 字符串 | 应用程序的名称。 |
| `userPerspective` | 字符串 | 事件发生时用户与应用程序或品牌之间的透视或物理关系。 了解用户对应用程序的看法有助于准确生成会话，因为大多数时间您不希望将`background`和`detached`事件作为“活动”会话的一部分包含在内。 此属性的值必须等于下面列出的枚举值之一。 <li> `foreground`:用户和应用程序之间直接交互。 </li> <li> `background`:App和用户间接互动。例如，应用程序可以测量一个值并在屏幕锁定或前景中使用另一个应用程序时刷新。  </li> <li> `detached`:Detached表示事件与应用程序相关，但并非直接来自应用程序，例如从外部系统发送电子邮件或推送通知。 |
| `version` | 字符串 | 应用程序的版本。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
