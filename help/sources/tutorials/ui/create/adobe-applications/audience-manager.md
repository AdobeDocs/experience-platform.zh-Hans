---
keywords: Experience Platform；主页；热门主题；受众管理器源连接器；Audience Manager;受众管理器连接器
solution: Experience Platform
title: 在UI中创建Adobe Audience Manager源连接
topic-legacy: overview
type: Tutorial
description: 本教程将指导您逐步创建一个源连接器，以便Adobe Audience Manager使用用户界面将消费者体验事件数据导入平台。
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 在UI中创建Adobe Audience Manager源连接

本教程将指导您逐步为Adobe Audience Manager创建源连接器，以便使用用户界面将Consumer Experience 事件数据导入平台。

## 使用Adobe Audience Manager创建源连接

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示了可为其创建帐户的各种源。

在[!UICONTROL Adobe applications]类别下，选择&#x200B;**[!UICONTROL Adobe Audience Manager]**，然后选择&#x200B;**[!UICONTROL Configure]**。

![目录](../../../../images/tutorials/create/aam/catalog.png)

此时将显示[!UICONTROL Select traits and segments]步骤，为您提供一个交互界面来浏览和选择您的特征、细分和数据。

* 接口的左面板包含[!UICONTROL Select traits and segments]选项以及可供您使用的所有区段的分层目录。
* 该界面的右半部分允许您与选定的区段进行交互，并挑选您要使用的特定数据。

![add-data](../../../../images/tutorials/create/aam/add-data.png)

要浏览可用区段，请从[!UICONTROL All Segments]面板中选择要访问的文件夹。 选择文件夹后，您可以遍历文件夹的层次结构，并提供一列表要筛选的区段。

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

确定并选择要使用的区段后，右侧将显示一个新面板，显示您对选定项目的列表。 您可以继续访问不同的文件夹，并为连接选择不同的区段。 选择更多区段会更新右侧的面板。

![select-data](../../../../images/tutorials/create/aam/select-data.png)

或者，您也可以选择&#x200B;**[!UICONTROL Select all segments]**&#x200B;和&#x200B;**[!UICONTROL Select all traits]**&#x200B;框。 选择所有区段会将Audience Manager区段引入平台，而选择所有特征则支持来自Audience Manager的所有第一方特征。

完成后，选择&#x200B;**[!UICONTROL Next]**

![所有细分](../../../../images/tutorials/create/aam/all-segments.png)

此时将显示[!UICONTROL Review]步骤，允许您在选定特征和区段连接到平台之前对其进行查看。 详细信息按以下类别分组：

* **[!UICONTROL Connection]**:显示源平台和连接状态。
* **[!UICONTROL Selected data]**:显示选定区段和启用特征的数量。

![审查](../../../../images/tutorials/create/aam/review.png)

查看数据流后，请选择&#x200B;**[!UICONTROL Finish]**&#x200B;并允许一段时间创建数据流。

## 后续步骤

当Audience Manager数据流处于活动状态时，传入数据会自动被引入实时客户用户档案。 您现在可以使用此传入数据，并使用平台分段服务创建受众区段。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../../../../profile/home.md)
* [分段服务概述](../../../../../segmentation/home.md)
