---
keywords: Experience Platform；主页；热门主题；分析；分类
description: 了解如何在UI中创建Adobe Analytics源连接器，以将分类数据引入Adobe Experience Platform。
solution: Experience Platform
title: 在UI中为分类数据创建Adobe Analytics Source连接
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 在UI中为分类数据创建Adobe Analytics源连接

本教程提供了在UI中创建Adobe Analytics分类数据源连接的步骤，以便将分类数据导入Adobe Experience Platform。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md)：Experience Platform提供了将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

Analytics Classifications Data Connector要求在使用之前，将您的数据迁移到Adobe Analytics的新[!DNL Classifications]基础架构。 要确认数据的迁移状态，请联系您的Adobe客户团队。

## 选择您的分类

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问源工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示用于创建入站连接的可用源。 每个源卡都会显示一个选项，用于配置新帐户或将数据添加到现有帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要处理的特定源。

在&#x200B;**[!UICONTROL Adobe应用程序]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;卡，然后选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以开始使用Analytics分类数据。

![](../../../../images/tutorials/create/classifications/catalog.png)

出现&#x200B;**[!UICONTROL Analytics源添加数据]**&#x200B;步骤。 从顶部标题中选择&#x200B;**[!UICONTROL 分类]**&#x200B;以查看[!DNL Classifications]数据集的列表，包括有关其维度ID、报表包名称和报表包ID的信息。

每个页面最多可显示10个您可以从中选择的不同[!DNL Classifications]数据集。 选择页面底部的&#x200B;**[!UICONTROL 下一步]**&#x200B;以浏览更多选项。 右侧的面板显示您选择的[!DNL Classifications]数据集的总数及其名称。 此面板还允许您删除任何可能不小心选择的[!DNL Classifications]数据集，或通过一次操作清除所有选择。

您最多可以选择30个不同的[!DNL Classifications]数据集以引入[!DNL Platform]。

选择[!DNL Classifications]数据集后，在页面的右上角选择&#x200B;**[!UICONTROL 下一步]**。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 查看分类

将显示&#x200B;**[!UICONTROL 审核]**&#x200B;步骤，允许您在创建选定[!DNL Classifications]数据集之前对其进行审核。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源平台和连接的状态。
* **[!UICONTROL 数据类型]**：显示选定的[!DNL Classifications]数。
* **[!UICONTROL 正在计划]**：显示[!DNL Classifications]数据的同步频率。

查看数据流后，单击&#x200B;**[!UICONTROL 完成]**&#x200B;并留出一些时间来创建数据流。

![](../../../../images/tutorials/create/classifications/review.png)

## 监测分类数据流

创建数据流后，您可以监控通过它摄取的数据。 从&#x200B;**[!UICONTROL 目录]**&#x200B;屏幕中，选择&#x200B;**[!UICONTROL 数据流]**&#x200B;以查看与您的[!DNL Classifications]帐户关联的已建立流的列表。

![](../../../../images/tutorials/create/classifications/dataflows.png)

出现&#x200B;**[!UICONTROL 数据流]**&#x200B;屏幕。 本页是一个数据流列表，包括有关其名称、源数据和数据流运行状态的信息。 右侧是包含有关[!DNL Classifications]数据流的元数据的&#x200B;**[!UICONTROL 属性]**&#x200B;面板。

选择要访问的&#x200B;**[!UICONTROL 目标数据集]**。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

**[!UICONTROL 数据集活动]**&#x200B;页面显示有关所选目标数据集的信息，包括其批处理状态、数据集ID和架构的详细信息。

![](../../../../images/tutorials/create/classifications/dataset.png)

## 后续步骤

通过学习本教程，您已创建一个Analytics Classifications Data Connector，可将[!DNL Classifications]数据引入[!DNL Platform]。 有关[!DNL Analytics]和[!DNL Classifications]数据的详细信息，请参阅以下文档：

* [Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md)
* [在UI中创建Analytics数据连接](./analytics.md)
* [关于分类](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
