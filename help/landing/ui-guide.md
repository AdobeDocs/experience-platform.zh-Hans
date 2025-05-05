---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform；用户指南；ui指南；平台ui指南；平台简介；功能板；
solution: Experience Platform
title: Experience Platform UI概述
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 1%

---

# Adobe Experience Platform UI指南

本指南提供了使用Adobe Experience Platform用户界面(UI)的简介，说明了各种组件的用途，并提供了指向更多相关文档的链接。

若要了解有关Adobe Experience Platform的更多信息，请阅读[Experience Platform概述](home.md)。

## 主屏幕

登录Adobe Experience Platform后，您位于[!UICONTROL 主页]页面，该页面由[指标仪表板](#metrics)、[最近数据](#recent-data)和[推荐学习](#recommended-learning)部分组成。

![](images/user-guide/homepage.png)

### 量度

量度仪表板提供一些信息卡，可向您提供有关贵组织内的数据集、配置文件、区段和目标的信息。

![](images/user-guide/homepage-dashboard.png)

**[!UICONTROL 数据集]**&#x200B;部分显示组织内的数据集数。 此数字将在创建新数据集时更新。 您可以在[数据集概述](../catalog/datasets/overview.md)中找到有关数据集的更多信息。

**[!UICONTROL 配置文件]**&#x200B;部分显示贵组织中具有配置文件（不包括配置文件片段）的总人数。 此总人数表示可寻址受众总数，每24小时更新一次。 您可以在[实时客户个人资料概述](../profile/home.md)中找到有关个人资料的更多信息。

**[!UICONTROL 区段]**&#x200B;部分显示在您的组织内创建的区段总数。 此数字将在创建新区段时更新。 您可以在[分段服务概述](../segmentation/home.md)中找到有关区段的更多信息。

**[!UICONTROL 目标]**&#x200B;部分显示为组织创建的目标总数。 此数字将在创建新目标时更新。 您可以在[目标概述](../destinations/home.md)中找到有关目标的更多信息。

### 最新数据

最近的数据仪表板提供有关最近创建的数据集、源、区段和目标的信息。

![](images/user-guide/homepage-recent.png)

**[!UICONTROL 最近数据集]**&#x200B;部分列出了贵组织内最近创建的五个数据集。 每次创建新数据集时，此列表都会更新。 您可以从列表中选择要查看的数据集可以查找有关指定数据集的详细信息，也可以选择&#x200B;**[!UICONTROL 查看全部]**&#x200B;以查看所有已创建的数据集的列表。 您可以在[数据集概述](../catalog/datasets/overview.md)中找到有关数据集的更多信息。

**[!UICONTROL 最近的源]**&#x200B;部分列出了组织中最近创建的五个源连接器。 每次创建新源连接器时，此列表都会更新。 您可以从列表中选择要查看的源连接您可以找到有关指定连接器的详细信息，也可以选择&#x200B;**[!UICONTROL 查看全部]**&#x200B;查看所有已创建的源连接的列表。 您可以在[源概述](../sources/home.md)中找到有关源的更多信息。

**[!UICONTROL 最近的区段]**&#x200B;部分列出了组织中最近创建的五个区段定义。 每次创建新区段定义时，此列表都会更新。 您可以从列表中选择要查看的区段定义您可以找到有关指定区段定义的详细信息，也可以选择&#x200B;**[!UICONTROL 查看全部]**&#x200B;以查看所有已创建区段定义的列表。 您可以在[分段服务概述](../segmentation/home.md)中找到有关区段的更多信息。

**[!UICONTROL 最近的目标]**&#x200B;部分列出了组织中最近创建的五个目标。 每次创建新目标时，此列表都会更新。 您可以从列表中选择要查看的目标您可以找到有关指定目标的详细信息，也可以选择&#x200B;**[!UICONTROL 查看全部]**&#x200B;查看所有已创建目标的列表。 您可以在[目标概述](../destinations/home.md)中找到有关目标的更多信息。

### 推荐学习

**[!UICONTROL 推荐学习]**&#x200B;部分提供了指向有用文档的链接以开始使用Adobe Experience Platform。

![](images/user-guide/homepage-recommended.png)

## 顶部导航栏

Experience Platform UI中的顶部导航栏显示您当前登录到的组织，并提供几个重要控件。

导航栏的左侧是Adobe Experience Platform徽标。 随时选择此徽标可让您回到Experience Platform UI主屏幕。

![](./images/user-guide/homepage-top-nav-bar.png)

### 组织切换器

顶部导航栏右侧的第一个项目是&#x200B;**组织切换器**。

![](./images/user-guide/homepage-ims-org-switcher.png)

选择切换器会打开一个下拉菜单，其中包含您有权访问的组织（如果有）。 要切换到其他组织，请选择列出的选项。

### 切换应用程序

顶部导航右侧的下一个项目是&#x200B;**应用程序切换器**，由![应用程序切换器](/help/images/icons/apps.png)图标表示。 选择此图标后，您可以在贵组织有权访问的Adobe应用程序(如Experience Platform、Analytics、Assets和其他应用程序)之间进行切换。

### 帮助

应用程序切换器的右侧是&#x200B;**帮助和支持菜单**，它由![问号/帮助](/help/images/icons/help.png)图标表示。 选择此图标后，会显示一个弹出菜单，其中包含多个帮助和支持资源。 **[!UICONTROL 帮助]**&#x200B;选项卡显示当前所在页面的相关文档列表。 “**[!UICONTROL 支持]**”选项卡允许您与Adobe支持团队创建支持票证。 通过&#x200B;**[!UICONTROL 反馈]**&#x200B;选项卡，可向Adobe提交有关Experience Platform的反馈。

![](images/user-guide/homepage-help-clicked.png)

### 通知和公告

在&#x200B;**通知部分**&#x200B;中，由![铃铛/通知和公告](/help/images/icons/bell.png)图标表示。 **[!UICONTROL 通知]**&#x200B;选项卡显示有关产品的重要信息以及其他相关更新，而&#x200B;**[!UICONTROL 公告]**&#x200B;选项卡显示有关服务维护的信息。

### 用户配置文件

顶部导航栏上的最后一个项目是&#x200B;**用户设置**，由![用户设置/用户配置文件](images/user-guide/profile-icon.png)图标表示。 选择此图标以编辑您的首选项或注销。

您可以使用位于您的姓名和电子邮件正下方的开关在Experience Platform界面的浅色和深色主题之间切换。 选择您喜欢的主题。

![](images/theme.png)

### 沙盒

顶部导航栏的正下方是沙盒栏。 此栏显示您当前用于Experience Platform的沙盒。 您可以在[沙盒概述](../sandboxes/home.md)中找到有关沙盒的更多信息。

## 左侧导航栏 {#left-nav}

屏幕左侧的导航会列出Experience Platform UI中支持的所有不同服务。

单击菜单图标可显示或隐藏左侧导航面板。

![](images/user-guide/hidemenu.png)

显示面板后，再次单击可将导航锁定在打开位置。

>[!IMPORTANT]
>
>左侧导航栏仅显示您可以访问的功能。 在Adobe Experience Platform的早期版本中，禁用了不可用的项目。 如果您认为您应该有权访问未显示的部分，请联系您的系统管理员。

![](images/user-guide/homepage-left.png)

通过&#x200B;**[!UICONTROL 主页]**&#x200B;部分，可返回Experience Platform UI主页。

**[!UICONTROL 工作流]**&#x200B;部分显示了用于在Experience Platform中执行操作的多步骤工作流列表。 您可以在[工作流概述](./workflows.md)中找到有关工作流的更多信息。

### [!UICONTROL 连接]

**[!UICONTROL 源]**&#x200B;部分允许您创建、更新和删除源连接，从而允许您将外部源中的数据摄取到Experience Platform中。 您可以在[源概述](../sources/home.md)中找到有关源的更多信息。

通过&#x200B;**[!UICONTROL 目标]**&#x200B;部分，您可以创建、更新和删除目标，以便将数据从Experience Platform导出到多个外部目标。 您可以在[目标概述](../destinations/home.md)中找到有关目标的更多信息。

### [!UICONTROL 客户]

**[!UICONTROL 配置文件]**&#x200B;部分允许您浏览客户配置文件、查看配置文件量度、创建和管理合并策略以及查看合并架构。 若要了解有关使用[!UICONTROL 配置文件]部分的更多信息，请阅读[[!DNL Profile] 用户指南](../profile/ui/user-guide.md)。 您可以在[实时客户配置文件概述](../profile/home.md)中找到有关实时客户配置文件的更多信息。

**[!UICONTROL 受众]**&#x200B;部分允许您创建和管理区段定义。 若要了解有关使用[!UICONTROL 受众]部分的更多信息，请阅读[分段用户指南](../segmentation/ui/overview.md)。 您可以在[分段服务概述](../segmentation/home.md)中找到有关分段服务的更多信息。

通过&#x200B;**[!UICONTROL 身份]**&#x200B;部分，您可以创建和管理身份命名空间。 有关[!UICONTROL 身份]部分的更多信息，包括身份命名空间以及如何在Experience Platform UI中使用身份的信息，请参阅[身份命名空间概述](../identity-service/features/namespaces.md)。

### [!UICONTROL Privacy]

**[!UICONTROL 策略]**&#x200B;部分允许您创建和管理数据使用策略。 若要了解有关使用“策略”部分的更多信息，请阅读[数据使用策略用户指南](../data-governance/policies/user-guide.md)。 您可以在[数据使用策略概述](../data-governance/policies/overview.md)中找到有关数据使用策略的更多信息。

通过&#x200B;**[!UICONTROL 请求]**&#x200B;部分，您可以创建和管理隐私请求。 请注意，您必须列入允许列表才能访问Privacy Service UI。 若要了解有关使用“请求”部分的更多信息，请阅读[Privacy Service用户指南](../privacy-service/ui/user-guide.md)。 您可以在[Privacy Service概述](../privacy-service/home.md)中找到有关Privacy Service的更多信息。

### [!UICONTROL 数据科学]

**[!UICONTROL Notebooks]**&#x200B;部分提供了对JupyterLab的访问，这是一个交互式开发环境，允许您探索、分析和建模数据。 若要了解有关使用“笔记本”部分的更多信息，请阅读[JupyterLab用户指南](../data-science-workspace/jupyterlab/overview.md)。 您可以在[数据科学Workspace概述](../data-science-workspace/home.md)中找到有关数据科学Workspace的更多信息

**[!UICONTROL 模型]**&#x200B;部分允许您使用机器学习和人工智能来创建、开发、训练和调整模型以进行预测。 您可以在有关[培训的教程中找到有关“模型”部分的详细信息，并评估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

通过&#x200B;**[!UICONTROL 服务]**&#x200B;部分，您可以管理已发布的模型以进行计划的培训和评分，或使用Adobe的智能服务（一组提供实时、个性化客户体验的AI服务）。 您可以在[将模型发布为服务教程](../data-science-workspace/models-recipes/publish-model-service-ui.md)中找到有关“服务”部分的更多信息。

### [!UICONTROL 数据管理]

通过&#x200B;**[!UICONTROL 架构]**&#x200B;部分，您可以创建和管理Experience Data Model (XDM)架构。 若要了解有关架构的更多信息，请阅读有关[创建架构](../xdm/tutorials/create-schema-ui.md)的教程。 您可以在[XDM系统概述](../xdm/home.md)中找到有关XDM的更多信息。

**[!UICONTROL 数据集]**&#x200B;部分允许您创建和管理数据集。 您可以在[数据集用户指南](../catalog/datasets/user-guide.md)中找到有关数据集的更多信息。

**[!UICONTROL 查询]**&#x200B;部分允许您创建和管理查询，记录由Adobe Experience Platform查询服务发出的SQL查询，以及查看您的[!DNL PostgreSQL]凭据。 您可以在[查询服务用户指南](../query-service/ui/overview.md)中找到有关查询的详细信息。

通过&#x200B;**[!UICONTROL 监控]**&#x200B;部分，您可以监控批次和流式摄取。 您可以在[监视数据摄取用户指南](../ingestion/quality/monitor-data-ingestion.md)中找到有关监视的详细信息。

### [!UICONTROL 联合数据]

**[!UICONTROL 模型]**&#x200B;部分允许您设计和创建定义数据的结构、关系和约束的数据模型和架构。 您可以在[联合受众组合用户指南](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/config/datamodel/schemas)中找到有关数据模型和架构的更多信息。

**[!UICONTROL 审核跟踪]**&#x200B;部分提供了已实时对您的环境执行的所有操作和事件的详细时间顺序记录。 您可以在[联合受众组合用户指南](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/audit-trail/audit-trail)中找到有关审核跟踪的详细信息。


通过&#x200B;**[!UICONTROL 联合数据库]**&#x200B;部分，您可以将Adobe Experience Platform连接到企业数据仓库。 您可以在[联合受众组合用户指南](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/config/federated-db)中找到有关连接到联合数据库的详细信息。

### [!UICONTROL 决策]

Adobe Journey Optimizer是基于Experience Platform构建的应用程序服务。 它允许您使用强大的决策技术，在适当的时间通过所有接触点为客户提供最佳优惠和体验。 要了解有关Journey Optimizer的更多信息，包括使用[!UICONTROL 优惠]和[!UICONTROL 活动]，请访问[Journey Optimizer文档](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hans)。

### [!UICONTROL 管理]

Experience Platform用户界面(UI)提供了一个仪表板，通过该仪表板可以查看有关您组织的许可证使用情况的重要信息，在每日快照期间捕获了这些信息。 通过在导航中选择&#x200B;**[!UICONTROL 许可证使用情况]**&#x200B;来访问此仪表板。 若要了解有关许可证使用情况仪表板的详细信息，请访问[许可证使用情况仪表板指南](./license-usage-and-guardrails/license-usage-dashboard.md)。

>[!IMPORTANT]
>
>许可证使用情况仪表板功能当前为Alpha版，并非对所有用户都可用。 文档和功能可能会发生变化。

## 后续步骤

通过阅读本指南，我们向您介绍了Experience Platform UI的主页和主要导航元素。 有关在用户界面中工作的更多详细信息，请参阅每个Experience Platform服务的文档。 在本文档前面的[左侧导航](#left-nav)部分提供了指向此文档的链接。
