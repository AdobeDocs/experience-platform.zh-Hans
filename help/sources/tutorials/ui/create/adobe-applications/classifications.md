---
keywords: Experience Platform；主页；热门主题；分析；分类
description: 本教程提供了在UI中创建Adobe Analytics分类数据连接器以将分类数据引入Adobe Experience Platform的步骤。
solution: Experience Platform
title: 在UI中创建Adobe Analytics分类数据连接器
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 在UI中创建Adobe Analytics分类数据连接器

本教程提供了在UI中创建Adobe Analytics分类数据连接器以将分类数据引入Adobe Experience Platform的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

Analytics Classifications Data Connector要求您的数据在使用前已迁移到Adobe Analytics新的[!DNL Classifications]基础架构。 要确认Adobe的迁移状态，请联系您的客户成功经理。

## 选择您的分类

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问源工作区。 **[!UICONTROL 目录]**&#x200B;屏幕显示可用源，用于创建入站连接。 每个源卡都显示一个选项，用于配置新帐户或向现有帐户添加数据。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL Adobe应用程序]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;卡，然后选择&#x200B;**[!UICONTROL 将数据]**&#x200B;添加到使用分析分类数据的开始。

![](../../../../images/tutorials/create/classifications/catalog.png)

出现&#x200B;**[!UICONTROL 分析源添加数据]**&#x200B;步骤。 从顶部标题中选择&#x200B;**[!UICONTROL 分类]**&#x200B;可查看[!DNL Classifications]数据集的列表，包括有关其维度ID、报表包名称和报表包ID的信息。

每页最多显示十个不同的[!DNL Classifications]数据集。 选择页面底部的&#x200B;**[!UICONTROL 下一页]**&#x200B;以浏览更多选项。 右侧的面板显示您选择的[!DNL Classifications]数据集的总数及其名称。 此面板还允许您删除您可能错误选择的任何[!DNL Classifications]数据集，或通过一个操作清除所有选择。

最多可以选择30个不同的[!DNL Classifications]数据集以引入[!DNL Platform]。

选择[!DNL Classifications]数据集后，请选择页面右上方的&#x200B;**[!UICONTROL 下一步]**。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 查看分类

出现&#x200B;**[!UICONTROL 查看]**&#x200B;步骤，允许您在创建所选[!DNL Classifications]数据集之前查看该数据集。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源平台和连接状态。
* **[!UICONTROL 数据类型]**:显示选定的数量 [!DNL Classifications]。
* **[!UICONTROL 计划]**:显示数据的同步 [!DNL Classifications] 频率。

查看数据流后，单击&#x200B;**[!UICONTROL 完成]**&#x200B;并允许一段时间创建数据流。

![](../../../../images/tutorials/create/classifications/review.png)

## 监视分类数据流

创建数据流后，您可以监视通过它摄取的数据。 从&#x200B;**[!UICONTROL 目录]**&#x200B;屏幕中，选择&#x200B;**[!UICONTROL 数据流]**&#x200B;以视图与[!DNL Classifications]帐户关联的已建立流的列表。

![](../../../../images/tutorials/create/classifications/dataflows.png)

出现&#x200B;**[!UICONTROL 数据流]**&#x200B;屏幕。 本页是数据流的列表，包括有关其名称、源数据和数据流运行状态的信息。 右侧是&#x200B;**[!UICONTROL 属性]**&#x200B;面板，其中包含与[!DNL Classifications]数据流相关的元数据。

选择要访问的&#x200B;**[!UICONTROL 目标数据集]**。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

**[!UICONTROL 数据集活动]**&#x200B;页显示有关您选择的目标数据集的信息，包括有关其批处理状态、数据集ID和模式的详细信息。

>[!IMPORTANT]
>
>虽然其他源连接器可以删除数据集，但Analytics Classifications Data Connector当前不支持此功能。 如果您误删除了数据集，请与Adobe客户服务部联系。

![](../../../../images/tutorials/create/classifications/dataset.png)


## 后续步骤

按照本教程，您创建了一个Analytics Classifications Data连接器，它将[!DNL Classifications]数据引入[!DNL Platform]。 有关[!DNL Analytics]和[!DNL Classifications]数据的详细信息，请参阅以下文档:

* [Analytics数据连接器概述](../../../../connectors/adobe-applications/analytics.md)
* [在UI中创建Analytics数据连接器](./analytics.md)
* [关于分类](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)