---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Adobe Analytics源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建Adobe Analytics源连接器

本教程提供了在UI中创建Adobe Analytics源连接器以将消费者数据导入Adobe Experience Platform的步骤。

## 使用Adobe Analytics创建源连接

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏 **中选择源** ，以访问源工作区。 “目 *录* ”屏幕显示用于创建绑定连接的可用源，每个源显示与它们关联的现有连接的数量。 选择 **Adobe Analytics的选项** ，然后单击 **视图源** ，以查看与它建立的所有绑定连接。

![](../../../../images/tutorials/create/analytics/AA-sources_catalog.png)

“源 *活动* ”屏幕列表所有以前建立的Adobe Analytics连接，您可以通过单击“选择数据”创建新 **连接**。

>[!NOTE] 可以与源建立多个绑定连接以引入不同的数据。

![](../../../..//images/tutorials/create/analytics/AA-source_activity.png)

从可用报表包的列表中，选择要引入平台的报表包，然后单击“下 **一步”**。

>[!NOTE] 每个Analytics源连接只能选择一个报告套件。 此外，只有一个报告套件只能存在于一个沙箱中。

![](../../../../images/tutorials/create/analytics/AA-select_data.png)

此时 *会显示* “审阅”步骤，允许您在创建新的Analytics绑定连接之前对其进行审阅。 连接的详细信息按类别分组，包括：

* *源详细信息*:显示源连接的类型和选定的报表包。
* *目标详细信息*:创建其他源连接器时，此容器显示源数据要摄取到的数据集，包括数据集所附加的模式。 分析数据会自动映射并引入实时客户用户档案。

![](../../../../images/tutorials/create/analytics/AA-review.png)

## 后续步骤

创建连接后，将自动创建目标模式和数据集以包含传入的数据。 此外，还会进行数据回填，并收集长达13个月的历史数据。 初始摄取完成时，Analytics数据将被下游平台服务(如实时客户用户档案和细分服务)使用。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../../../../profile/home.md)
* [分段服务概述](../../../../../segmentation/home.md)
* [数据科学工作区概述](../../../../../data-science-workspace/home.md)
* [查询服务概述](../../../../../query-service/home.md)

