---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform；用户指南；ui指南；平台ui指南；平台简介；仪表板；
solution: Experience Platform
title: Experience PlatformUI概述
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 1%

---

# Adobe Experience Platform UI指南

本指南提供了使用Adobe Experience Platform用户界面(UI)的简介，说明了各种组件的用途，并提供了指向更多相关文档的链接。

要进一步了解Adobe Experience Platform，请阅读 [Experience Platform概述](home.md).

## 主屏幕

登录Adobe Experience Platform后，您可以在 [!UICONTROL 主页] 页面，由 [量度仪表板](#metrics)， [最新数据](#recent-data)、和 [推荐学习](#recommended-learning) 部分。

![](images/user-guide/homepage.png)

### 量度

量度仪表板提供一些信息卡，可向您提供有关贵组织内的数据集、配置文件、区段和目标的信息。

![](images/user-guide/homepage-dashboard.png)

此 **[!UICONTROL 数据集]** 部分显示组织内的数据集数。 此数字将在创建新数据集时更新。 有关数据集的更多信息，请参阅 [数据集概述](../catalog/datasets/overview.md).

此 **[!UICONTROL 配置文件]** 部分显示贵组织中具有配置文件的人员总数，不包括配置文件片段。 此总人数表示可寻址受众总数，每24小时更新一次。 有关用户档案的更多信息，请参阅 [Real-time Customer Profile概述](../profile/home.md).

此 **[!UICONTROL 区段]** 部分显示在您的组织内创建的区段总数。 此数字将在创建新区段时更新。 有关区段的更多信息，请参阅 [分段服务概述](../segmentation/home.md).

此 **[!UICONTROL 目标]** 部分显示为组织创建的目标总数。 此数字将在创建新目标时更新。 有关目标的更多信息，请参阅 [目标概述](../destinations/home.md).

### 最新数据

最近的数据仪表板提供有关最近创建的数据集、源、区段和目标的信息。

![](images/user-guide/homepage-recent.png)

此 **[!UICONTROL 最近数据集]** 部分列出了贵组织内最近创建的五个数据集。 每次创建新数据集时，此列表都会更新。 您可以从列表中选择一个数据集以查看有关指定数据集的更多信息，或选择 **[!UICONTROL 查看全部]** 查看所有已创建数据集的列表。 有关数据集的更多信息，请参阅 [数据集概述](../catalog/datasets/overview.md).

此 **[!UICONTROL 最近的源]** 部分列出了贵组织内最近创建的五个源连接器。 每次创建新源连接器时，此列表都会更新。 您可以从列表中选择源连接以查看有关指定连接器的详细信息，或选择 **[!UICONTROL 查看全部]** 查看所有已创建的源连接的列表。 欲知关于来源的更多信息，请参见 [源概述](../sources/home.md).

此 **[!UICONTROL 最近的区段]** 部分列出了组织中最近创建的五个区段定义。 每次创建新区段定义时，此列表都会更新。 您可以从列表中选择段定义，以查看有关指定段定义的详细信息，或选择 **[!UICONTROL 查看全部]** 以查看所有已创建的区段定义的列表。 有关区段的更多信息，请参阅 [分段服务概述](../segmentation/home.md).

此 **[!UICONTROL 最近的目标]** 部分列出了贵组织中最近创建的五个目标。 每次创建新目标时，此列表都会更新。 您可以从列表中选择一个目标以查看有关指定目标的详细信息，或选择 **[!UICONTROL 查看全部]** 查看所有已创建目标的列表。 有关目标的更多信息，请参阅 [目标概述](../destinations/home.md).

### 推荐学习

此 **[!UICONTROL 推荐学习]** 部分提供了指向有用文档的链接，以便开始使用Adobe Experience Platform。

![](images/user-guide/homepage-recommended.png)

## 顶部导航栏

Platform UI中的顶部导航栏显示您当前登录的组织，并提供几个重要控件。

导航栏的左侧是Adobe Experience Platform徽标。 您随时可以通过选择此徽标回到Platform UI主屏幕。

![](./images/user-guide/homepage-top-nav-bar.png)

### 组织切换器

顶部导航栏右侧的第一个项目是 **组织切换器**.

![](./images/user-guide/homepage-ims-org-switcher.png)

选择切换器会打开一个下拉菜单，其中包含您有权访问的组织（如果有）。 要切换到其他组织，请选择列出的选项。

### 切换应用程序

顶部导航右侧的下一个项目是 **应用程序切换器**，由 ![应用程序切换器](./images/user-guide/app-switcher-icon.png) 图标。 选择此图标后，您可以在组织有权访问的Adobe应用程序(如Experience Platform、Analytics、资源等)之间进行切换。

### 帮助

应用程序切换器的右侧是 **帮助和支持菜单**，由 ![问号/帮助](./images/user-guide/help-icon.png) 图标。 选择此图标后，会显示一个弹出菜单，其中包含多个帮助和支持资源。 此 **[!UICONTROL 帮助]** 选项卡会显示与您当前所在页面相关的文档列表。 此 **[!UICONTROL 支持]** 选项卡允许您与Adobe支持团队一起创建支持工单。 此 **[!UICONTROL 反馈]** 选项卡允许您将有关Platform的反馈提交给Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知和公告

在 **通知部分**，由 ![铃铛/通知和公告](images/user-guide/notification-icon.png) 图标。 此 **[!UICONTROL 通知]** 选项卡会显示有关产品的重要信息以及其他相关更新，而 **[!UICONTROL 公告]** 选项卡显示有关服务维护的信息。

### 用户配置文件

顶部导航栏上的最后一个项目是 **用户设置**，由 ![用户设置/用户配置文件](images/user-guide/profile-icon.png) 图标。 选择此图标以编辑您的首选项或注销。

您可以使用位于您姓名和电子邮件正下方的开关，在Platform界面的浅色和深色主题之间切换。 选择您喜欢的主题。

![](images/theme.png)

### 沙盒

顶部导航栏的正下方是沙盒栏。 此栏显示您当前用于Platform的沙盒。 有关沙箱的详细信息，请参阅 [沙盒概述](../sandboxes/home.md).

## 左侧导航栏 {#left-nav}

屏幕左侧的导航会列出Platform UI中支持的所有不同服务。

单击菜单图标可显示或隐藏左侧导航面板。

![](images/user-guide/hidemenu.png)

显示面板后，再次单击可将导航锁定在打开位置。

>[!IMPORTANT]
>
>左侧导航栏仅显示您可以访问的功能。 在Adobe Experience Platform的早期版本中，禁用了不可用的项目。 如果您认为您应该有权访问未显示的部分，请联系您的系统管理员。

![](images/user-guide/homepage-left.png)

此 **[!UICONTROL 主页]** 部分允许您返回到Platform UI主页。

此 **[!UICONTROL 工作流]** 部分显示了用于在Platform内执行操作的多步骤工作流列表。 有关工作流的更多信息，请参阅 [工作流概述](./workflows.md).

### [!UICONTROL 连接]

此 **[!UICONTROL 源]** 部分允许您创建、更新和删除源连接，以便将数据从外部源摄取到Platform中。 欲知关于来源的更多信息，请参见 [源概述](../sources/home.md).

此 **[!UICONTROL 目标]** 部分允许您创建、更新和删除目标，以便能够将数据从Platform导出到多个外部目标。 有关目标的更多信息，请参阅 [目标概述](../destinations/home.md).

### [!UICONTROL 客户]

此 **[!UICONTROL 配置文件]** 部分允许您浏览客户配置文件，查看配置文件量度，创建和管理合并策略，以及查看合并架构。 要了解有关使用 [!UICONTROL 配置文件] 部分，请阅读 [[!DNL Profile] 用户指南](../profile/ui/user-guide.md). 有关Real-time Customer Profile的更多信息，请参见 [Real-time Customer Profile概述](../profile/home.md).

此 **[!UICONTROL 区段]** 部分允许您创建和管理区段定义。 要了解有关使用 [!UICONTROL 区段] 部分，请阅读 [分段用户指南](../segmentation/ui/overview.md). 欲知关于分段服务的更多信息，请参见 [分段服务概述](../segmentation/home.md).

此 **[!UICONTROL 身份]** 部分允许您创建和管理身份命名空间。 欲知关于 [!UICONTROL 身份] 部分，包括有关身份命名空间以及如何在Platform UI中使用身份的信息，请参阅 [身份命名空间概述](../identity-service/features/namespaces.md).

### [!UICONTROL Privacy]

此 **[!UICONTROL 策略]** 部分允许您创建和管理数据使用策略。 要了解有关使用策略部分的更多信息，请阅读 [数据使用策略用户指南](../data-governance/policies/user-guide.md). 有关数据使用策略的更多信息，请参阅 [数据使用策略概述](../data-governance/policies/overview.md).

此 **[!UICONTROL 请求]** 部分允许您创建和管理隐私请求。 请注意，您必须列入允许列表才能访问Privacy ServiceUI。 要了解有关使用请求部分的更多信息，请阅读 [Privacy Service用户指南](../privacy-service/ui/user-guide.md). 有关Privacy Service的更多信息，请参阅 [Privacy Service概述](../privacy-service/home.md).

### [!UICONTROL 数据科学]

此 **[!UICONTROL Notebooks]** 部分提供对JupyterLab的访问，它是一个交互式开发环境，允许您探索、分析和建模数据。 要了解有关使用笔记本部分的更多信息，请阅读 [JupyterLab用户指南](../data-science-workspace/jupyterlab/overview.md). 有关数据科学工作区的更多信息，请参阅 [数据科学工作区概述](../data-science-workspace/home.md)

此 **[!UICONTROL 模型]** 部分允许您使用机器学习和人工智能创建、开发、训练和调整模型以进行预测。 有关“模型”部分的更多信息，请参阅的教程 [训练和评估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

此 **[!UICONTROL 服务]** 通过部分，您可以管理已发布的模型以进行计划的训练和评分，或使用Adobe的智能服务（一组提供实时、个性化客户体验的AI服务）。 有关“服务”部分的更多信息，请参见 [将模型发布为服务教程](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL 数据管理]

此 **[!UICONTROL 架构]** 部分允许您创建和管理Experience Data Model (XDM)架构。 要了解有关架构的更多信息，请阅读以下内容的教程： [创建架构](../xdm/tutorials/create-schema-ui.md). 有关XDM的更多信息，请参阅 [XDM系统概述](../xdm/home.md).

此 **[!UICONTROL 数据集]** 部分允许您创建和管理数据集。 有关数据集的更多信息，请参阅 [数据集用户指南](../catalog/datasets/user-guide.md).

此 **[!UICONTROL 查询]** 部分允许您创建和管理查询，记录由Adobe Experience Platform查询服务发出的SQL查询，并查看您的 [!DNL PostgreSQL] 凭据。 有关查询的更多信息，请参阅 [查询服务用户指南](../query-service/ui/overview.md).

此 **[!UICONTROL 监控]** 部分允许您监视批量摄取和流式摄取。 有关监控的详细信息，请参见 [监控数据引入用户指南](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL 决策]

Adobe Journey Optimizer是基于Experience Platform构建的应用程序服务。 它允许您使用强大的决策技术，在适当的时间通过所有接触点为客户提供最佳优惠和体验。 详细了解Journey Optimizer，包括使用 [!UICONTROL 选件] 和 [!UICONTROL 活动] 访问 [Journey Optimizer文档](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hans).

### [!UICONTROL 管理]

Platform用户界面(UI)提供了一个仪表板，通过该仪表板可以查看有关您组织的许可证使用情况的重要信息，在每日快照期间捕获了这些信息。 通过选择 **[!UICONTROL 许可证使用情况]** 在导航中。 要了解有关许可证使用情况仪表板的更多信息，请访问 [许可证使用情况仪表板指南](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>许可证使用情况仪表板功能当前为Alpha版，并非对所有用户都可用。 文档和功能可能会发生变化。

## 后续步骤

通过阅读本指南，您现在已了解到Platform UI的主页和主要导航元素。 有关在用户界面中工作的更多详细信息，请参阅各个平台服务的文档。 此文档的链接在以下位置提供： [左侧导航](#left-nav) 部分包含在此文档的前面。
