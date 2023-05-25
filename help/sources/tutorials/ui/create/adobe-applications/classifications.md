---
keywords: Experience Platform；主页；热门主题；分析；分类
description: 了解如何在UI中创建Adobe Analytics源连接器，以将分类数据引入Adobe Experience Platform。
solution: Experience Platform
title: 在UI中为分类数据创建Adobe Analytics源连接
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 6%

---

# 在UI中为分类数据创建Adobe Analytics源连接

本教程提供了在UI中创建Adobe Analytics分类数据源连接的步骤，以便将分类数据引入Adobe Experience Platform。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

Analytics Classifications Data Connector要求您的数据已迁移到新的 [!DNL Classifications] Adobe Analytics的基础架构。 要确认数据的迁移状态，请联系您的Adobe客户团队。

## 选择您的分类

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问“源”工作区。 此 **[!UICONTROL 目录]** 屏幕显示用于创建入站连接的可用源。 每个源卡都显示一个选项，用于配置新帐户或将数据添加到现有帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL Adobe应用程序]** 类别，选择 **[!UICONTROL Adobe Analytics]** 信息卡，然后选择 **[!UICONTROL 添加数据]** 以开始使用Analytics分类数据。

![](../../../../images/tutorials/create/classifications/catalog.png)

此 **[!UICONTROL Analytics源添加数据]** 步骤。 选择 **[!UICONTROL 分类]** 以查看 [!DNL Classifications] 数据集，包括有关其维度ID、报表包名称和报表包ID的信息。

每个页面最多可显示十个不同的页面 [!DNL Classifications] 您可以从中进行选择的数据集。 选择 **[!UICONTROL 下一个]** 以浏览更多选项。 右侧的面板显示 [!DNL Classifications] 您选择的数据集及其名称。 此面板还允许您删除任何 [!DNL Classifications] 您可能错误地选择了数据集，或通过一次操作清除所有选择。

您最多可以选择30个不同的 [!DNL Classifications] 要引入的数据集 [!DNL Platform].

选择您的 [!DNL Classifications] 数据集，选择 **[!UICONTROL 下一个]** 页面右上角的。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 查看分类

此 **[!UICONTROL 审核]** 步骤，允许您查看所选内容 [!DNL Classifications] 数据集。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源平台和连接状态。
* **[!UICONTROL 数据类型]**：显示选择的数量 [!DNL Classifications].
* **[!UICONTROL 计划]**：显示同步的频率 [!DNL Classifications] 数据。

查看数据流后，单击 **[!UICONTROL 完成]** 并留出一些时间来创建数据流。

![](../../../../images/tutorials/create/classifications/review.png)

## 监测分类数据流

创建数据流后，您可以监控通过它摄取的数据。 从 **[!UICONTROL 目录]** 屏幕，选择 **[!UICONTROL 数据流]** 要查看与您的关联的已建立流的列表，请执行以下操作 [!DNL Classifications] 帐户。

![](../../../../images/tutorials/create/classifications/dataflows.png)

此 **[!UICONTROL 数据流]** 屏幕。 在此页面上是一个数据流列表，其中包括有关其名称、源数据和数据流运行状态的信息。 右边是 **[!UICONTROL 属性]** 包含有关您的页面的元数据的面板 [!DNL Classifications] 数据流。

选择 **[!UICONTROL 目标数据集]** 您希望访问。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

此 **[!UICONTROL 数据集活动]** 页面显示有关所选目标数据集的信息，包括有关其批次状态、数据集ID和架构的详细信息。

>[!IMPORTANT]
>
>尽管其他源连接器可以删除数据集，但目前不支持 Analytics Classifications Data Connector 这样做。如果您误删除了一个数据集，请联系 Adobe 客户关怀部门。

![](../../../../images/tutorials/create/classifications/dataset.png)


## 后续步骤

通过学习本教程，您已创建一个Analytics Classifications Data Connector，它可以 [!DNL Classifications] 数据进入 [!DNL Platform]. 请参阅以下文档，了解更多有关 [!DNL Analytics] 和 [!DNL Classifications] 数据：

* [Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md)
* [在UI中创建Analytics数据连接](./analytics.md)
* [关于分类](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
