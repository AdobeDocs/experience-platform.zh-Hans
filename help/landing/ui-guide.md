---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform；用户指南；UI指南；平台UI指南；平台简介；功能板；
solution: Experience Platform
title: Experience PlatformUI概述
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 3%

---

# Adobe Experience Platform UI指南

本指南是关于使用Adobe Experience Platform用户界面(UI)的简介，其中说明了各个组件的用途，并提供了指向更多文档的链接以了解更多信息。

要了解有关Adobe Experience Platform的更多信息，请阅读[Experience Platform概述](home.md)。

## 主屏幕

登录Adobe Experience Platform后，您位于[!UICONTROL Home]页面，该页面由[量度功能板](#metrics)、[最近数据](#recent-data)和[建议学习](#recommended-learning)部分组成。

![](images/user-guide/homepage.png)

### 量度

量度功能板提供了信息卡，用于提供有关组织内的数据集、用户档案、区段和目标的信息。

![](images/user-guide/homepage-dashboard.png)

**[!UICONTROL Datasets]**&#x200B;部分显示IMS组织内的数据集数量。 此数字会在创建新数据集时更新。 有关数据集的更多信息，请参阅[数据集概述](../catalog/datasets/overview.md)。

**[!UICONTROL Profiles]**&#x200B;部分显示IMS组织内具有用户档案的总人数，不包括用户档案片段。 此总人数表示可寻址受众总数，每24小时更新一次。 有关用户档案的更多信息，请参阅[Real-time Customer Profile overview](../profile/home.md)。

**[!UICONTROL 区段]**&#x200B;部分显示在IMS组织内创建的区段总数。 此数字会在创建新区段时更新。 有关区段的更多信息，请参阅[Segmentation Service概述](../segmentation/home.md)。

**[!UICONTROL 目标]**&#x200B;部分显示为IMS组织创建的目标总数。 此数字将在创建新目标时更新。 有关目标的更多信息，请参阅[目标概述](../destinations/home.md)。

### 近期数据

最近的数据功能板提供有关最近创建的数据集、源、区段和目标的信息。

![](images/user-guide/homepage-recent.png)

**[!UICONTROL 最近的数据集]**&#x200B;部分列出了IMS组织内最近创建的五个数据集。 每次创建新数据集时，此列表都会更新。 您可以从列表中选择一个数据集以查看有关指定数据集的更多信息，或选择&#x200B;**[!UICONTROL 查看所有]**&#x200B;以查看所有创建数据集的列表。 有关数据集的更多信息，请参阅[数据集概述](../catalog/datasets/overview.md)。

**[!UICONTROL 最近的源]**&#x200B;部分列出了IMS组织内最近创建的五个源连接器。 每次创建新源连接器时，此列表都会更新。 您可以从列表中选择源连接以查看有关指定连接器的更多信息，或选择&#x200B;**[!UICONTROL 查看所有]**&#x200B;以查看所有创建的源连接的列表。 有关源的详细信息，请参阅[源概述](../sources/home.md)。

**[!UICONTROL 最近的区段]**&#x200B;部分列出了IMS组织内最近创建的五个区段定义。 每次创建新区段定义时，此列表都会更新。 您可以从列表中选择区段定义以查看有关指定区段定义的更多信息，或选择&#x200B;**[!UICONTROL 查看所有]**&#x200B;以查看所有创建的区段定义的列表。 有关区段的更多信息，请参阅[Segmentation Service概述](../segmentation/home.md)。

**[!UICONTROL 最近的目标]**&#x200B;部分列出了您的IMS组织内最近创建的五个目标。 每次创建新目标时，此列表都会更新。 您可以从列表中选择一个目标以查看有关指定目标的更多信息，或选择&#x200B;**[!UICONTROL 查看所有]**&#x200B;以查看所有已创建目标的列表。 有关目标的更多信息，请参阅[目标概述](../destinations/home.md)。

### 推荐学习

**[!UICONTROL 建议学习]**&#x200B;部分提供了指向有用文档的链接，以便开始使用Adobe Experience Platform。

![](images/user-guide/homepage-recommended.png)

## 顶部导航栏

Platform UI中的顶部导航栏会显示您当前已登录的IMS组织，并提供一些重要控件。

导航栏左侧是Adobe Experience Platform徽标。 随时选择此选项将返回Platform UI主屏幕。

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS组织切换器

顶部导航栏右侧的第一个项目是&#x200B;**IMS组织切换器**。

![](./images/user-guide/homepage-ims-org.png)

选择切换器会打开一个包含您有权访问的IMS组织的下拉菜单（如果有）。 选择一个列出的选项，以切换到该IMS组织。

![](./images/user-guide/homepage-ims-org-switcher.png)

### 切换应用程序

顶部导航右侧的下一个项目是&#x200B;**应用程序切换器**，由![应用程序切换器](./images/user-guide/app-switcher-icon.png)图标表示。 当您选择此图标时，您可以在IMS组织有权访问的Adobe应用程序(如Experience Platform、分析、资产等)之间切换。

### 帮助

应用程序切换器右侧是&#x200B;**帮助和支持菜单**，该菜单由![问号/帮助](./images/user-guide/help-icon.png)图标表示。 选择此图标时，会显示一个弹出菜单，其中包含多个帮助和支持资源。 **[!UICONTROL Help]**&#x200B;选项卡显示当前页面的相关文档列表。 **[!UICONTROL 支持]**&#x200B;选项卡允许您与Adobe支持团队一起创建支持票证。 **[!UICONTROL Feedback]**&#x200B;选项卡允许您将有关Platform的反馈提交到Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知和公告

在&#x200B;**通知部分**&#x200B;中，由![铃声/通知和公告](images/user-guide/notification-icon.png)图标表示。 **[!UICONTROL 通知]**&#x200B;选项卡显示有关产品和其他相关更新的重要信息，而&#x200B;**[!UICONTROL 公告]**&#x200B;选项卡显示有关服务维护的信息。

### 用户配置文件

顶部导航栏上的最后一项是&#x200B;**用户设置**，该设置由![用户设置/用户配置文件](images/user-guide/profile-icon.png)图标表示。 选择此图标可编辑首选项或注销。

### 沙盒

沙盒栏紧靠顶部导航栏的下方。 此栏显示您当前用于Platform的沙箱。 有关沙箱的更多信息，请参阅[沙箱概述](../sandboxes/home.md)。

## 左侧导航 {#left-nav}

屏幕左侧的导航列出了Platform UI中支持的所有不同服务。

>[!IMPORTANT]
>
>左侧导航栏上的某些部分可能未显示或呈灰显状态。 这是因为您无权访问这些功能。 如果您认为您应该有权访问这些部分，请联系您的系统管理员。

![](images/user-guide/homepage-left.png)

通过&#x200B;**[!UICONTROL Home]**&#x200B;部分可返回Platform UI主页。

**[!UICONTROL Workflows]**&#x200B;部分显示用于在Platform中执行操作的多步工作流的列表。 有关工作流的更多信息，请参阅[工作流概述](./workflows.md)。

### [!UICONTROL 连接]

通过&#x200B;**[!UICONTROL Sources]**&#x200B;部分，您可以创建、更新和删除源连接，从而将数据从外部源摄取到平台。 有关源的详细信息，请参阅[源概述](../sources/home.md)。

通过&#x200B;**[!UICONTROL 目标]**&#x200B;部分，您可以创建、更新和删除目标，从而将数据从Platform导出到许多外部目标。 有关目标的更多信息，请参阅[目标概述](../destinations/home.md)。

### [!UICONTROL 客户]

通过&#x200B;**[!UICONTROL Profiles]**&#x200B;部分，您可以浏览客户配置文件、查看配置文件量度、创建和管理合并策略以及查看合并架构。 要了解有关使用[!UICONTROL Profiles]部分的更多信息，请阅读[[!DNL Profile] 用户指南](../profile/ui/user-guide.md)。 有关实时客户资料的更多信息，请参阅[实时客户资料概述](../profile/home.md)。

通过&#x200B;**[!UICONTROL 区段]**&#x200B;部分，可以创建和管理区段定义。 要了解有关使用[!UICONTROL 区段]部分的更多信息，请阅读[分段用户指南](../segmentation/ui/overview.md)。 有关Segmentation Service的更多信息，请参阅[Segmentation Service概述](../segmentation/home.md)。

通过&#x200B;**[!UICONTROL Identities]**&#x200B;部分，可以创建和管理身份命名空间。 有关[!UICONTROL Identities]部分的更多信息，包括有关身份命名空间以及如何在Platform UI中使用身份的信息，请参阅[身份命名空间概述](../identity-service/namespaces.md)。

### [!UICONTROL 隐私]

通过&#x200B;**[!UICONTROL Policys]**&#x200B;部分，可以创建和管理数据使用策略。 要了解有关使用策略部分的更多信息，请阅读[数据使用策略用户指南](../data-governance/policies/user-guide.md)。 有关数据使用策略的更多信息，请参阅[数据使用策略概述](../data-governance/policies/overview.md)。

通过&#x200B;**[!UICONTROL Requests]**&#x200B;部分，您可以创建和管理隐私请求。 请注意，必须列入允许列表您才能访问Privacy ServiceUI。 要了解有关使用“请求”部分的更多信息，请阅读[Privacy Service用户指南](../privacy-service/ui/user-guide.md)。 有关Privacy Service的更多信息，请参阅[Privacy Service概述](../privacy-service/home.md)。

### [!UICONTROL 数据科学]

**[!UICONTROL Notebooks]**&#x200B;部分提供对JupyterLab的访问，JupyterLab是一个交互式开发环境，可让您探索、分析和建模数据。 要了解有关使用笔记本部分的更多信息，请阅读[JupyterLab用户指南](../data-science-workspace/jupyterlab/overview.md)。 有关数据科学工作区的更多信息，请参阅[数据科学工作区概述](../data-science-workspace/home.md)

**[!UICONTROL 模型]**&#x200B;部分允许您利用机器学习和人工智能来创建、开发、训练和调整模型以进行预测。 有关“模型”部分的更多信息，请参阅[培训和评估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)的教程。

通过&#x200B;**[!UICONTROL 服务]**&#x200B;部分，您可以管理发布的模型以进行计划培训和评分，或利用Adobe的Intelligent Services（一组AI服务，可提供实时、个性化的客户体验）。 有关“服务”部分的更多信息，请参阅[发布模型作为服务教程](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

### [!UICONTROL 数据管理]

通过&#x200B;**[!UICONTROL 架构]**&#x200B;部分，您可以创建和管理Experience Data Model(XDM)架构。 要了解有关模式的更多信息，请阅读有关[创建模式](../xdm/tutorials/create-schema-ui.md)的教程。 有关XDM的更多信息，请参阅[XDM系统概述](../xdm/home.md)。

通过&#x200B;**[!UICONTROL Datasets]**&#x200B;部分，可以创建和管理数据集。 有关数据集的更多信息，请参阅[数据集用户指南](../catalog/datasets/user-guide.md)。

通过&#x200B;**[!UICONTROL Queryes]**&#x200B;部分，可以创建和管理查询、记录由Adobe Experience Platform查询服务发出的SQL查询，以及查看PostgreSQL凭据。 有关查询的更多信息，请参阅[查询服务用户指南](../query-service/ui/overview.md)。

通过&#x200B;**[!UICONTROL 监控]**&#x200B;部分，您可以监控批量摄取和流式摄取。 有关监控的更多信息，请参阅[监控数据摄取用户指南](../ingestion/quality/monitor-data-ingestion.md)。

### [!UICONTROL 决策]

Offer Decisioning 是与 Adobe Experience Platform 集成的一项应用程序服务。它允许您利用 Experience Platform 在恰当的时间在所有接触点为客户提供卓越的优惠和体验。要了解有关Offer decisioning的更多信息，包括使用[!UICONTROL Offers]和[!UICONTROL Activities]访问[Offer decisioning文档](https://experienceleague.adobe.com/docs/offer-decisioning.html)。

### [!UICONTROL 管理]

平台用户界面(UI)提供了一个功能板，您可以通过该功能板查看有关贵组织许可证使用情况的重要信息，这些信息是在每日快照期间捕获的。 可通过在导航中选择&#x200B;**[!UICONTROL 许可证使用情况]**&#x200B;来访问此设置。 要了解有关许可证使用功能板的更多信息，请访问[许可证使用功能板指南](license-usage-dashboard.md)。

>[!IMPORTANT]
>
>许可证使用功能板功能当前位于alpha中，并非所有用户都可用。 文档和功能可能会发生变化。

## 后续步骤

通过阅读本指南，您现在已介绍到Platform UI的主页和主要导航元素。 有关在用户界面中工作的更多详细信息，请参阅每个Platform服务的相关文档。 本文档的链接位于本文档前面的左侧导航](#left-nav)部分。[
