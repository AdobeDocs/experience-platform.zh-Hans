---
keywords: Experience Platform；主页；热门主题；Audience Manager源连接器；Audience Manager;Audience Manager连接器
title: 在UI中创建Adobe Audience Manager源连接
description: 本教程将指导您完成为Adobe Audience Manager创建源连接的步骤，以便使用用户界面将消费者体验事件数据导入Platform。
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 9cdb8933d166445bf41ed314d7ffc7d5762e1adb
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# 在UI中创建Adobe Audience Manager源连接

本教程将指导您完成为Adobe Audience Manager创建源连接器的步骤，以便使用用户界面将消费者体验事件数据导入Platform。

## 创建与Adobe Audience Manager的源连接

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以为其创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL Adobe应用程序]，选择 **[!UICONTROL Adobe Audience Manager]** 然后选择 **[!UICONTROL 设置]**.

![目录](../../../../images/tutorials/create/aam/catalog.png)

### 选择特征和区段

>[!NOTE]
>
>您无法将Audience Manager源中的区域数据摄取到Experience Platform。 如果您的Analytics用例需要区域数据，请使用 [Analytics源连接器](../adobe-applications/analytics.md).

的 [!UICONTROL 选择特征和区段] ，为您提供一个交互式界面来浏览和选择您的特征、区段和数据。

* 界面的左侧面板包含 [!UICONTROL 选择特征和区段] 选项，以及可供您使用的所有区段的分层目录。
* 界面的右半部分允许您与选定的区段进行交互，并选取要使用的特定数据。

![添加数据](../../../../images/tutorials/create/aam/add-data.png)

要在可用区段中导航，请从 [!UICONTROL 所有区段] 的上界。 通过选择文件夹，您可以遍历文件夹的层次结构，并为您提供要过滤的区段列表。

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

确定并选择要使用的区段后，右侧会显示一个新面板，其中显示了选定项目的列表。 您可以继续访问不同的文件夹，并为连接选择不同的区段。 选择更多区段会更新右侧的面板。

![select-data](../../../../images/tutorials/create/aam/select-data.png)

或者，您也可以选择 **[!UICONTROL 选择所有区段]** 和 **[!UICONTROL 选择所有特征]** 框中。 选择所有区段会将Audience Manager区段引入Platform，同时选择所有特征会启用Audience Manager中的所有第一方特征。

>[!WARNING]
>
>首次使用Audience Manager源将Audience Manager区段发送到Platform时，大量Audience Manager区段人口的摄取会直接影响用户档案总数。 这意味着选择所有区段可能会导致用户档案计数超过您的许可证使用权限。 请查看 [许可证使用许可](../../../../../dashboards/guides/license-usage.md) 继续之前。

完成后，选择 **[!UICONTROL 下一个]**

![所有区段](../../../../images/tutorials/create/aam/all-segments.png)

的 [!UICONTROL 审阅] 步骤，以便您在选定的特征和区段连接到Platform之前对其进行查看。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源平台和连接的状态。
* **[!UICONTROL 选定数据]**:显示选定区段和已启用特征的数量。

![审查](../../../../images/tutorials/create/aam/review.png)

审核数据流后，选择 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

## 后续步骤

当Audience Manager数据流处于活动状态时，传入数据会自动摄取到实时客户配置文件中。 您现在可以使用此传入数据，并使用平台分段服务创建受众区段。 有关更多详细信息，请参阅以下文档：

* [实时客户资料概述](../../../../../profile/home.md)
* [Segmentation Service概述](../../../../../segmentation/home.md)
