---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform；用户指南；ui指南；平台ui指南；平台简介；仪表板;
solution: Experience Platform
title: Experience PlatformUI概述
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 3%

---

# Adobe Experience Platform UI指南

本指南是使用Adobe Experience Platform用户界面(UI)的简介，其中说明了各种组件的用途并提供了指向进一步文档的链接以获取更多信息。

要了解有关Adobe Experience Platform的更多信息，请阅读[Experience Platform概述](home.md)。

## 主屏幕

登录Adobe Experience Platform后，您位于[!UICONTROL Home]页，该页由[度量仪表板](#metrics)、[最近数据](#recent-data)和[建议的学习](#recommended-learning)部分组成。

![](images/user-guide/homepage.png)

### 量度

“量度仪表板”提供卡片，可为您提供有关组织内数据集、用户档案、区段和目标的信息。

![](images/user-guide/homepage-dashboard.png)

**[!UICONTROL Datasets]**&#x200B;部分显示IMS组织内的数据集数。 此数字在创建新数据集时更新。 有关数据集的详细信息，请参阅[数据集概述](../catalog/datasets/overview.md)。

**[!UICONTROL Profiles]**&#x200B;部分显示IMS组织内具有用户档案的人员总数，不包括用户档案片段。 此总人数代表可寻址的总受众，每24小时更新一次。 有关用户档案的详细信息，请参阅[实时用户档案概述](../profile/home.md)。

**[!UICONTROL Segments]**&#x200B;部分显示在IMS组织内创建的区段总数。 此数字在创建新区段时更新。 有关区段的详细信息，请参阅[分段服务概述](../segmentation/home.md)。

**[!UICONTROL Destinations]**&#x200B;部分显示为IMS组织创建的目标总数。 创建新目标时会更新此编号。 有关目标的详细信息，请参阅[目标概述](../destinations/home.md)。

### 最近数据

最近的数据仪表板提供了有关最近创建的数据集、源、区段和目标的信息。

![](images/user-guide/homepage-recent.png)

**[!UICONTROL Recent datasets]**&#x200B;部分列表了您IMS组织中最近创建的五个数据集。 每次创建新列表集时，都会更新此数据集。 您可以从列表中选择一个数据集以视图有关指定数据集的更多信息，或选择&#x200B;**[!UICONTROL View all]**&#x200B;以查看所有已创建数据集的列表。 有关数据集的详细信息，请参阅[数据集概述](../catalog/datasets/overview.md)。

**[!UICONTROL Recent sources]**&#x200B;部分列表了您IMS组织内最近创建的五个源连接器。 每次创建新的源连接器时，都会更新此列表。 您可以从列表中选择源连接以视图有关指定连接器的更多信息，或选择&#x200B;**[!UICONTROL View all]**&#x200B;查看所有已创建源连接的列表。 有关源的详细信息，请参阅[源概述](../sources/home.md)。

**[!UICONTROL Recent segments]**&#x200B;部分列表了您IMS组织中最近创建的五个区段定义。 每次创建新区段定义时，都会更新此列表。 您可以从列表中选择区段定义，以视图有关指定区段定义的更多信息，或选择&#x200B;**[!UICONTROL View all]**&#x200B;查看所有已创建区段定义的列表。 有关区段的详细信息，请参阅[分段服务概述](../segmentation/home.md)。

**[!UICONTROL Recent destinations]**&#x200B;部分列表了您IMS组织中最近创建的五个目标。 每次创建新目标时，都会更新此列表。 您可以从列表中选择目标，以视图有关指定目标的更多信息，或选择&#x200B;**[!UICONTROL View all]**&#x200B;以查看所有已创建目标的列表。 有关目标的详细信息，请参阅[目标概述](../destinations/home.md)。

### 推荐学习

**[!UICONTROL Recommended learning]**&#x200B;部分提供了开始使用Adobe Experience Platform的有用文档的链接。

![](images/user-guide/homepage-recommended.png)

## 顶部导航栏

平台UI中的顶部导航栏显示您当前已登录的IMS组织，并提供几个重要控件。

导航栏的左侧是Adobe Experience Platform徽标。 随时选择此选项将返回平台UI主屏幕。

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS组织切换程序

顶部导航栏右侧的第一个项目是&#x200B;**IMS组织切换器**。

![](./images/user-guide/homepage-ims-org.png)

选择切换器后，将打开您有权访问的IMS组织（如果有）的下拉菜单。 选择列出的选项以切换到该IMS组织。

![](./images/user-guide/homepage-ims-org-switcher.png)

### 切换应用程序

顶部导航右侧的下一个项目是&#x200B;**应用程序切换器**，由![应用程序切换器](./images/user-guide/app-switcher-icon.png)图标表示。 选择此图标后，您可以在IMS组织有权访问的Adobe应用程序(如Experience Platform、分析、资产和启动)之间切换。

### 帮助

应用程序切换器右侧是&#x200B;**帮助和支持菜单**，该菜单由![问号/帮助](./images/user-guide/help-icon.png)图标表示。 选择此图标时，将显示一个弹出菜单，其中包含多个帮助和支持资源。 **[!UICONTROL Help]**&#x200B;选项卡显示当前页面的相关文档列表。 **[!UICONTROL Support]**&#x200B;选项卡允许您与Adobe支持团队一起创建支持票证。 **[!UICONTROL Feedback]**&#x200B;选项卡允许您将有关平台的反馈提交到Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知和通知

在&#x200B;**通知部分**&#x200B;中，由![ bell/Notifications and Noncuments](images/user-guide/notification-icon.png)图标表示。 **[!UICONTROL Notifications]**&#x200B;选项卡显示有关产品和其他相关更新的重要信息，而&#x200B;**[!UICONTROL Announcements]**&#x200B;选项卡显示有关服务维护的信息。

### 用户用户档案

顶部导航栏上的最后一项是&#x200B;**用户设置**，它由![用户设置/用户用户档案](images/user-guide/profile-icon.png)图标表示。 选择此图标可编辑您的首选项或注销。

### 沙盒

顶部导航栏的正下方是沙箱栏。 此条显示您当前正用于平台的沙箱。 有关沙箱的详细信息，请参阅[沙箱概述](../sandboxes/home.md)。

## 左导航{#left-nav}

屏幕左侧的导航将列表平台UI中支持的所有不同服务。

>[!IMPORTANT]
>
>左侧导航栏上的某些部分可能不显示或灰显。 这是因为您无权访问这些功能。 如果您认为您应有权访问这些部分，请与您的系统管理员联系。

![](images/user-guide/homepage-left.png)

通过&#x200B;**[!UICONTROL Home]**&#x200B;部分可返回平台UI主页。

**[!UICONTROL Workflows]**&#x200B;部分显示用于在平台内执行操作的多步骤工作流列表。 有关工作流的详细信息，请参阅[工作流概述](./workflows.md)。

### [!UICONTROL Connections]

通过&#x200B;**[!UICONTROL Sources]**&#x200B;部分，您可以创建、更新和删除源连接，从而将外部源中的数据引入平台。 有关源的详细信息，请参阅[源概述](../sources/home.md)。

通过&#x200B;**[!UICONTROL Destinations]**&#x200B;部分，您可以创建、更新和删除目标，从而将数据从平台导出到许多外部目标。 有关目标的详细信息，请参阅[目标概述](../destinations/home.md)。

### [!UICONTROL Customer]

通过&#x200B;**[!UICONTROL Profiles]**&#x200B;部分，您可以浏览用户档案、视图用户档案量度、创建和管理合并策略以及视图合并模式。 要了解有关使用[!UICONTROL Profiles]部分的更多信息，请阅读[[!DNL Profile] 用户指南](../profile/ui/user-guide.md)。 有关实时客户用户档案的更多信息，请参阅[实时客户用户档案概述](../profile/home.md)。

通过&#x200B;**[!UICONTROL Segments]**&#x200B;部分，可创建和管理区段定义。 要了解有关使用[!UICONTROL Segments]部分的更多信息，请阅读[分段用户指南](../segmentation/ui/overview.md)。 有关分段服务的详细信息，请参阅[分段服务概述](../segmentation/home.md)。

通过&#x200B;**[!UICONTROL Identities]**&#x200B;部分可创建和管理身份命名空间。 有关[!UICONTROL Identities]部分的详细信息，包括有关标识命名空间以及如何在平台UI中使用标识的信息，请参阅[标识命名空间概述](../identity-service/namespaces.md)。

### [!UICONTROL Privacy]

通过&#x200B;**[!UICONTROL Policies]**&#x200B;部分，可以创建和管理数据使用策略。 要了解有关使用“策略”部分的更多信息，请阅读[数据使用策略用户指南](../data-governance/policies/user-guide.md)。 有关数据使用策略的详细信息，请参阅[数据使用策略概述](../data-governance/policies/overview.md)。

通过&#x200B;**[!UICONTROL Requests]**&#x200B;部分，可创建和管理隐私请求。 请注意，必须列入允许列表您才能访问Privacy ServiceUI。 要了解有关使用“请求”部分的更多信息，请阅读[Privacy Service用户指南](../privacy-service/ui/user-guide.md)。 有关Privacy Service的详细信息，请参阅[Privacy Service概述](../privacy-service/home.md)。

### [!UICONTROL Data Science]

**[!UICONTROL Notebooks]**&#x200B;部分提供对JupyterLab的访问，JupyterLab是一个交互式开发环境，可让您探索、分析和建模数据。 要了解有关使用笔记本部分的更多信息，请阅读[JupyterLab用户指南](../data-science-workspace/jupyterlab/overview.md)。 有关数据科学工作区的详细信息，请参阅[数据科学工作区概述](../data-science-workspace/home.md)

通过&#x200B;**[!UICONTROL Models]**&#x200B;部分，您可以利用机器学习和人工智能创建、开发、培训和调整模型以进行预测。 有关“模型”部分的详细信息，请参阅[培训和评估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)的教程。

通过&#x200B;**[!UICONTROL Services]**&#x200B;部分，您可以管理发布的模型以进行计划培训和评分，或利用Adobe的智能服务，这是一组AI服务，可提供实时、个性化的客户体验。 有关“服务”部分的详细信息，请参阅[将模型作为服务发布教程](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

### [!UICONTROL Data management]

通过&#x200B;**[!UICONTROL Schemas]**&#x200B;部分，可创建和管理体验数据模型(XDM)模式。 要了解有关模式的更多信息，请阅读有关创建模式](../xdm/tutorials/create-schema-ui.md)的教程。 [有关XDM的详细信息，请参阅[XDM系统概述](../xdm/home.md)。

通过&#x200B;**[!UICONTROL Datasets]**&#x200B;部分可创建和管理数据集。 有关数据集的详细信息，请参阅[数据集用户指南](../catalog/datasets/user-guide.md)。

通过&#x200B;**[!UICONTROL Queries]**&#x200B;部分，可以创建和管理查询，记录Adobe Experience Platform 查询 Service创建的SQL查询，并视图您的PostgreSQL凭据。 有关查询的详细信息，请参阅[查询服务用户指南](../query-service/ui/overview.md)。

通过&#x200B;**[!UICONTROL Monitoring]**&#x200B;部分，可以监视批处理和流摄取。 有关监视的详细信息，请参阅[监视数据摄取用户指南](../ingestion/quality/monitor-data-ingestion.md)。

### [!UICONTROL Decisioning]

Offer Decisioning 是与 Adobe Experience Platform 集成的一项应用程序服务。它允许您利用 Experience Platform 在恰当的时间在所有接触点为客户提供卓越的优惠和体验。要进一步了解Offer decisioning，包括使用[!UICONTROL Offers]和[!UICONTROL Activities]，请访问[Offer decisioning文档](https://experienceleague.adobe.com/docs/offer-decisioning.html)。

### [!UICONTROL Administration]

平台用户界面(UI)提供了一个仪表板，通过它可以视图有关单位许可证使用情况的重要信息，这些信息在每日快照中捕获。 可通过在导航中选择&#x200B;**[!UICONTROL License usage]**&#x200B;来访问。 要了解有关许可证使用仪表板的更多信息，请访问[许可证使用仪表板指南](license-usage-dashboard.md)。

>[!IMPORTANT]
>
>许可证使用仪表板功能当前位于alpha中，并非所有用户都可用。 文档和功能可能会发生变化。

## 后续步骤

阅读本指南后，您现在已介绍平台UI的主页和主要导航元素。 有关在用户界面中工作的更多详细信息，请参阅各个平台服务的相关文档。 指向本文档的链接位于此文档前面的左侧导航](#left-nav)部分。[
