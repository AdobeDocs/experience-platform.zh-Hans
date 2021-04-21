---
keywords: Experience Platform；主页；热门主题；分析；分类
description: 了解如何在UI中创建Adobe Analytics源连接器以将分类数据引入Adobe Experience Platform。
solution: Experience Platform
title: 在UI中为分类数据创建Adobe Analytics源连接
topic-legacy: overview
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 在UI中为分类数据创建Adobe Analytics源连接

本教程提供了在UI中创建Adobe Analytics分类数据源连接以将分类数据引入Adobe Experience Platform的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

Analytics Classifications Data Connector要求您的数据在使用前已迁移到Adobe Analytics的新[!DNL Classifications]基础架构。 要确认Adobe的迁移状态，请联系您的客户成功经理。

## 选择分类

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问源工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示可用源，用于创建入站连接。 每个源卡都显示一个选项，用于配置新帐户或向现有帐户添加数据。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL Adobe applications]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;卡，然后选择&#x200B;**[!UICONTROL Add data]**&#x200B;以开始使用Analytics分类数据。

![](../../../../images/tutorials/create/classifications/catalog.png)

出现&#x200B;**[!UICONTROL Analytics source add data]**&#x200B;步骤。 从顶部标题中选择&#x200B;**[!UICONTROL Classifications]**&#x200B;以查看[!DNL Classifications]数据集的列表，包括有关其维度ID、报表包名称和报表包ID的信息。

每页最多显示十个不同的[!DNL Classifications]数据集。 选择页面底部的&#x200B;**[!UICONTROL Next]**&#x200B;以浏览更多选项。 右侧的面板显示您选择的[!DNL Classifications]数据集的总数及其名称。 此面板还允许您删除可能因错误选择的任何[!DNL Classifications]数据集，或通过一个操作清除所有选择。

您最多可以选择30个不同的[!DNL Classifications]数据集以导入[!DNL Platform]。

选择[!DNL Classifications]数据集后，请选择页面右上方的&#x200B;**[!UICONTROL Next]**。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 查看分类

将显示&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在创建所选[!DNL Classifications]数据集之前查看它。 详细信息按以下类别分组：

* **[!UICONTROL Connection]**:显示源平台和连接状态。
* **[!UICONTROL Data type]**:显示选定的数量 [!DNL Classifications]。
* **[!UICONTROL Scheduling]**:显示数据的同步 [!DNL Classifications] 频率。

查看数据流后，单击&#x200B;**[!UICONTROL Finish]**&#x200B;并允许一段时间创建数据流。

![](../../../../images/tutorials/create/classifications/review.png)

## 监视分类数据流

创建数据流后，您可以监视通过它摄取的数据。 从&#x200B;**[!UICONTROL Catalog]**&#x200B;屏幕中，选择&#x200B;**[!UICONTROL Dataflows]**&#x200B;以视图与[!DNL Classifications]帐户关联的已建立流的列表。

![](../../../../images/tutorials/create/classifications/dataflows.png)

出现&#x200B;**[!UICONTROL Dataflows]**&#x200B;屏幕。 本页是数据流的列表，包括有关其名称、源数据和数据流运行状态的信息。 右侧是&#x200B;**[!UICONTROL Properties]**&#x200B;面板，其中包含有关[!DNL Classifications]数据流的元数据。

选择要访问的&#x200B;**[!UICONTROL Target dataset]**。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

**[!UICONTROL Dataset activity]**&#x200B;页面显示有关您选择的目标数据集的信息，包括有关其批处理状态、数据集ID和模式的详细信息。

>[!IMPORTANT]
>
>虽然其他源连接器可以删除数据集，但Analytics Classifications数据连接器当前不支持删除数据集。 如果您误删了数据集，请与Adobe客户服务部联系。

![](../../../../images/tutorials/create/classifications/dataset.png)


## 后续步骤

通过本教程，您创建了一个Analytics Classifications Data连接器，它将[!DNL Classifications]数据引入[!DNL Platform]。 有关[!DNL Analytics]和[!DNL Classifications]数据的详细信息，请参阅以下文档:

* [Analytics数据连接器概述](../../../../connectors/adobe-applications/analytics.md)
* [在UI中创建Analytics数据连接](./analytics.md)
* [关于分类](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
