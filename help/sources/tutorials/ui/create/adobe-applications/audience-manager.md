---
keywords: Experience Platform；主页；热门主题；Audience Manager源连接器；Audience Manager；audience Manager连接器
title: 在UI中创建Adobe Audience Manager Source连接
description: 本教程将指导您完成以下步骤：创建Adobe Audience Manager的源连接，以便使用用户界面将消费者体验事件数据引入Experience Platform。
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 1%

---

# 在UI中创建Adobe Audience Manager源连接

本教程将指导您完成为Adobe Audience Manager创建源连接器的步骤，以便使用用户界面将消费者体验事件数据引入Experience Platform。

## 创建与Adobe Audience Manager的源连接

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在[!UICONTROL Adobe应用程序]下，选择&#x200B;**[!UICONTROL Adobe Audience Manager]**，然后选择&#x200B;**[!UICONTROL 设置]**。

![目录](../../../../images/tutorials/create/aam/catalog.png)

### 选择特征和区段

>[!NOTE]
>
>您无法从Audience Manager源将区域数据摄取到Experience Platform。 如果您的Analytics用例需要区域数据，请使用[Analytics源连接器](../adobe-applications/analytics.md)。

此时将显示[!UICONTROL 选择特征和区段]步骤，该步骤为您提供了一个交互式界面来探索和选择特征、区段和数据。

* 界面的左侧面板包含[!UICONTROL 选择特征和区段]选项，以及所有可用区段的分层目录。
* 利用界面的右半部分，可与选定的区段进行交互，并选取要使用的特定数据。

![添加数据](../../../../images/tutorials/create/aam/add-data.png)

要浏览可用区段，请从[!UICONTROL 所有区段]面板中选择要访问的文件夹。 选择文件夹允许您遍历文件夹的层次结构，并为您提供要过滤的区段列表。

![区段文件夹](../../../../images/tutorials/create/aam/segment-folder.png)

标识并选择要使用的区段后，右侧将显示一个新面板，其中显示选定项目的列表。 您可以继续访问不同的文件夹，并为连接选择不同的区段。 选择更多区段将更新右侧的面板。

![select-data](../../../../images/tutorials/create/aam/select-data.png)

或者，也可以选择&#x200B;**[!UICONTROL 选择所有区段]**&#x200B;和&#x200B;**[!UICONTROL 选择所有特征]**&#x200B;框。 选择所有区段会将Audience Manager区段引入Experience Platform，而选择所有特征会启用Audience Manager中的所有第一方特征。

>[!WARNING]
>
>当您首次使用Audience Manager源将Audience Manager区段发送到Experience Platform时，大量Audience Manager区段人口的摄取会直接影响您的总配置文件计数。 这意味着选择所有区段可能会导致配置文件计数超过您的许可证使用授权。 请在继续之前检查您的[许可证使用限额](../../../../../dashboards/guides/license-usage.md)。

完成后，选择&#x200B;**[!UICONTROL 下一步]**

![所有区段](../../../../images/tutorials/create/aam/all-segments.png)

将显示[!UICONTROL 审核]步骤，允许您在选定特征和区段连接到Experience Platform之前对其进行审核。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源平台和连接的状态。
* **[!UICONTROL 选定数据]**：显示选定区段数和启用的特征数。

![审核](../../../../images/tutorials/create/aam/review.png)

查看数据流后，选择&#x200B;**[!UICONTROL 完成]**，然后等待一些时间来创建数据流。

## 后续步骤

在Audience Manager数据流处于活动状态时，传入数据会自动摄取到实时客户档案中。 您现在可以利用这些传入数据，并使用Experience Platform分段服务来创建受众区段。 有关更多详细信息，请参阅以下文档：

* [实时客户轮廓概述](../../../../../profile/home.md)
* [分段服务概述](../../../../../segmentation/home.md)
