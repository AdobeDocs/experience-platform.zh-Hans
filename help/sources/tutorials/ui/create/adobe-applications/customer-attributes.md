---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建客户属性源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建客户属性源连接器

本教程提供了在UI中创建源连接器的步骤，用于收集将数据用户档案到Adobe Experience Platform的客户属性。 有关客户属性的详细信息，请参阅概 [述文档](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/customer-attributes/attributes.html)。

## 创建源连接

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏 **中选择源** ，以访问源工作区。 “目 *录* ”屏幕显示用于创建入站连接的可用源，每个源显示与它们关联的现有连接数。 选择“客户属性” **选项** ，然后单击“ **Connect源”**。 如果连接成功，您将被重定向，以便建立连接。

>[!NOTE] 如果您已经为客户属性用户档案数据建立了源连接器，则将禁用与源连接的选项。

![](../../../../images/tutorials/create/customer-attributes/CA-sources_catalog.png)

“源 *活动* ”屏幕列表客户属性用户档案数据的所有先前建立的连接，您可以通过单击“选择数据”创建新 **连接**。

>[!NOTE] 可以建立与源的多个入站连接以引入不同的数据。

![](../../../../images/tutorials/create/customer-attributes/CA-source_activity.png)

从可用客户属性用户档案数据集的列表中，选择要引入平台的数据集，然后单击“下 **一步”**。

>[!NOTE] 每个客户属性源连接只能选择一个数据集。

![](../../../../images/tutorials/create/customer-attributes/CA-select_data.png)

将显 *示“审阅* ”步骤，允许您在创建新的入站连接之前查看该连接。 连接的详细信息按类别分组，包括：

* *源详细信息*:显示源连接的类型和所选源数据。
* *目标详细信息*:创建其他源连接器时，此容器显示源数据要摄取到的数据集，包括数据集所附加的模式。 客户属性用户档案数据会自动映射并摄取到实时客户用户档案中。

![](../../../../images/tutorials/create/customer-attributes/CA-review.png)

## 后续步骤

创建连接后，将自动创建目标模式和数据集以包含传入的数据。 当初始摄取完成时，下游平台服务(如实时客户用户档案和细分服务)可以使用客户属性用户档案数据。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../../../../profile/home.md)
* [分段服务概述](../../../../../segmentation/home.md)
