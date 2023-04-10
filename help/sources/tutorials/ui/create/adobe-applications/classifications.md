---
keywords: Experience Platform；主页；热门主题；分析；分类
description: 了解如何在UI中创建Adobe Analytics源连接器以将分类数据引入Adobe Experience Platform。
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

本教程提供了在UI中创建Adobe Analytics分类数据源连接以将分类数据导入Adobe Experience Platform的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

Analytics分类数据连接器要求您的数据已迁移到 [!DNL Classifications] Adobe Analytics基础设施。 要确认数据的迁移状态，请联系您的Adobe帐户团队。

## 选择分类

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 来访问源工作区。 的 **[!UICONTROL 目录]** 屏幕显示用于创建入站连接的可用源。 每个源卡都显示一个选项，用于配置新帐户或将数据添加到现有帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL Adobe应用程序]** 类别，选择 **[!UICONTROL Adobe Analytics]** 卡片，然后选择 **[!UICONTROL 添加数据]** 开始使用Analytics分类数据。

![](../../../../images/tutorials/create/classifications/catalog.png)

的 **[!UICONTROL Analytics源添加数据]** 中。 选择 **[!UICONTROL 分类]** 从顶部标题查看 [!DNL Classifications] 数据集，包括有关其维度ID、报表包名称和报表包ID的信息。

每个页面最多显示10个不同的页面 [!DNL Classifications] 您可以从中选择的数据集。 选择 **[!UICONTROL 下一个]** 以浏览更多选项。 右侧的面板显示 [!DNL Classifications] 您选择的数据集及其名称。 此面板还允许您删除 [!DNL Classifications] 您可能错误选择的数据集，或通过一项操作清除所有选择。

您最多可以选择30个不同的 [!DNL Classifications] 数据集引入 [!DNL Platform].

选择 [!DNL Classifications] 数据集，选择 **[!UICONTROL 下一个]** 页面右上方。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 查看分类

的 **[!UICONTROL 审阅]** 步骤，以便您查看所选内容 [!DNL Classifications] 数据集创建之前生成的数据集。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源平台和连接的状态。
* **[!UICONTROL 数据类型]**:显示选定的数量 [!DNL Classifications].
* **[!UICONTROL 计划]**:显示同步的频率 [!DNL Classifications] 数据。

审核数据流后，单击 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

![](../../../../images/tutorials/create/classifications/review.png)

## 监控分类数据流

创建数据流后，您可以监控通过其摄取的数据。 从 **[!UICONTROL 目录]** 屏幕，选择 **[!UICONTROL 数据流]** 查看与 [!DNL Classifications] 帐户。

![](../../../../images/tutorials/create/classifications/dataflows.png)

的 **[!UICONTROL 数据流]** 屏幕。 本页提供了数据流列表，包括有关其名称、源数据和数据流运行状态的信息。 右边是 **[!UICONTROL 属性]** 包含与 [!DNL Classifications] 数据流。

选择 **[!UICONTROL Target数据集]** 您希望访问。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

的 **[!UICONTROL 数据集活动]** “页面”显示有关您选择的目标数据集的信息，包括有关其批处理状态、数据集ID和架构的详细信息。

>[!IMPORTANT]
>
>尽管其他源连接器可以删除数据集，但目前不支持 Analytics Classifications Data Connector 这样做。如果您误删除了一个数据集，请联系 Adobe 客户关怀部门。

![](../../../../images/tutorials/create/classifications/dataset.png)


## 后续步骤

通过阅读本教程，您创建了一个Analytics分类数据连接器，该连接器 [!DNL Classifications] 数据输入 [!DNL Platform]. 有关 [!DNL Analytics] 和 [!DNL Classifications] 数据：

* [Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md)
* [在UI中创建Analytics数据连接](./analytics.md)
* [关于分类](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
