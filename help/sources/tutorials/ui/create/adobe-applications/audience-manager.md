---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Adobe受众管理器源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建Adobe受众管理器源连接器

本教程将指导您逐步创建Adobe受众管理器的源连接器，以便使用用户界面将消费者体验事件数据导入平台。

## 使用Adobe受众管理器创建源连接

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏 **中选择源** ，以访问源工作区。 “目 *录* ”屏幕显示各种源，您可以为这些源创建源连接，每个源显示与它们关联的现有连接数。

在 *Adobe应用程序类别下* ，选择 **Adobe受众管理器** ，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及视图其文档或与源连接的选项。

要为Adobe受众管理器创建新的源连接器，请单击“ **Connect源”**。

![](../../../../images/tutorials/create/aam/aam_catalog.png)

将显示一个对话框。 单击 **Connect** 以创建连接。

![](../../../../images/tutorials/create/aam/aam_connect_full.png)

如果与Adobe受众管理器建立了源连接，则会显示受众管 *理器连接器的* “源活动”页面。

![](../../../../images/tutorials/create/aam/aam_flow.png)

如果要暂停传入的受众管理器数据，可以通过单击数据流列表并从右侧的“属性”列切换 *其* “状 *态* ”。

![](../../../../images/tutorials/create/aam/aam_flow_disable.png)

## 后续步骤

当受众管理器数据流处于活动状态时，传入数据会自动被引入实时客户用户档案。 您现在可以使用传入的数据，并使用平台分段服务创建受众细分。 有关更多详细信息，请参阅以下文档:

- [实时客户用户档案概述](../../../../../profile/home.md)
- [分段服务概述](../../../../../segmentation/home.md)