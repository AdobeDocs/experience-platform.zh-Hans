---
keywords: Experience Platform；主页；热门主题；Audience Manager源连接器；Audience Manager；Audience Manager连接器
title: 在UI中创建Adobe Audience Manager源连接
description: 本教程将指导您完成为Adobe Audience Manager创建源连接的步骤，以便使用用户界面将消费者体验事件数据引入Platform。
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# 在UI中创建Adobe Audience Manager源连接

本教程将指导您完成为Adobe Audience Manager创建源连接器的步骤，以便使用用户界面将消费者体验事件数据引入Platform。

## 创建与Adobe Audience Manager的源连接

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

下 [!UICONTROL Adobe应用程序]，选择 **[!UICONTROL Adobe Audience Manager]** 然后选择 **[!UICONTROL 设置]**.

![目录](../../../../images/tutorials/create/aam/catalog.png)

### 选择特征和区段

>[!NOTE]
>
>您无法从Audience Manager源摄取区域数据到Experience Platform。 如果您的Analytics用例需要区域数据，请使用 [Analytics源连接器](../adobe-applications/analytics.md).

此 [!UICONTROL 选择特征和区段] 步骤随即显示，为您提供一个交互式界面，用于浏览和选择您的特征、区段和数据。

* 界面的左侧面板包含 [!UICONTROL 选择特征和区段] 选项以及所有可用区段的分层目录。
* 利用界面的右半部分，可与选定的区段进行交互并浏览要使用的特定数据。

![add-data](../../../../images/tutorials/create/aam/add-data.png)

要浏览可用区段，请从中选择要访问的文件夹 [!UICONTROL 所有区段] 面板。 选择文件夹允许您遍历文件夹的层次结构，并会为您提供要过滤的区段列表。

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

标识并选择要使用的区段后，右侧将显示一个新面板，其中显示选定项目的列表。 您可以继续访问不同的文件夹，并为连接选择不同的区段。 选择更多区段将更新右侧的面板。

![select-data](../../../../images/tutorials/create/aam/select-data.png)

或者，您也可以选择 **[!UICONTROL 选择所有区段]** 和 **[!UICONTROL 选择所有特征]** 盒子。 选择所有区段会将Audience Manager区段引入Platform，而选择所有特征会启用来自Audience Manager的所有第一方特征。

>[!WARNING]
>
>当您首次使用Audience Manager源向Platform发送Audience Manager区段时，大量的Audience Manager区段群体的摄取会直接影响您的总配置文件计数。 这意味着选择所有区段可能会导致配置文件计数超过您的许可证使用授权。 请查看您的 [许可证使用限额](../../../../../dashboards/guides/license-usage.md) 然后再继续。

完成后，选择 **[!UICONTROL 下一个]**

![所有区段](../../../../images/tutorials/create/aam/all-segments.png)

此 [!UICONTROL 审核] 步骤，允许您在选定特征和区段连接到Platform之前查看它们。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源平台和连接状态。
* **[!UICONTROL 选定的数据]**：显示选定的区段数和启用的特征数。

![审核](../../../../images/tutorials/create/aam/review.png)

查看数据流后，选择 **[!UICONTROL 完成]** 并留出一些时间来创建数据流。

## 后续步骤

当Audience Manager数据流处于活动状态时，传入数据将自动摄取到Real-Time Customer Profiles中。 您现在可以利用这些传入数据，并使用Platform Segmentation Service创建受众区段。 有关更多详细信息，请参阅以下文档：

* [Real-time Customer Profile概述](../../../../../profile/home.md)
* [分段服务概述](../../../../../segmentation/home.md)
