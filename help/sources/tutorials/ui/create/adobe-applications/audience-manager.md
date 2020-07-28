---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Adobe Audience Manager源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 2%

---


# 在UI中创建Adobe Audience Manager源连接器

本教程将指导您逐步创建源连接器，供Adobe Audience Manager使用，以便使用用户界面将消费者体验事件数据导入平台。

## 使用Adobe Audience Manager创建源连接

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **侧导航栏** 中选择“源”以访问源工作区。 “目 *录* ”屏幕显示可为其创建源连接的各种源，每个源显示与它们关联的现有连接数。

在Adobe *应用程序* 类别下，选择 **Adobe Audience Manager** ，以在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及视图其文档或与源连接的选项。

要创建新的源连接器进行Adobe Audience Manager，请单击“ **连接源”**。

![](../../../../images/tutorials/create/aam/aam_catalog.png)

将显示一个对话框。单 **击** “连接”创建连接。

![](../../../../images/tutorials/create/aam/aam_connect_full.png)

如果已建立与Adobe Audience Manager的源连接，则显 *示Audience Manager* 连接器的“源活动”页。

![](../../../../images/tutorials/create/aam/aam_flow.png)

如果要暂停传入Audience Manager数据，可以单击流列表，并从右侧的“属性”列 *切换* 其“状 *态* ”。

![](../../../../images/tutorials/create/aam/aam_flow_disable.png)

## 后续步骤

当Audience Manager数据流处于活动状态时，传入数据会自动引入实时客户用户档案。 您现在可以使用此传入数据，并使用平台分段服务创建受众段。 有关更多详细信息，请参阅以下文档:

- [实时客户用户档案概述](../../../../../profile/home.md)
- [分段服务概述](../../../../../segmentation/home.md)