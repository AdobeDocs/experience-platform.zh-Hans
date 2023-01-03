---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform；用户指南；UI指南；平台UI指南；平台简介；功能板；
solution: Experience Platform
title: Experience PlatformUI概述
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 1%

---

# Adobe Experience Platform UI指南

本指南是关于使用Adobe Experience Platform用户界面(UI)的简介，其中说明了各个组件的用途，并提供了指向更多文档的链接以了解更多信息。

要了解有关Adobe Experience Platform的更多信息，请阅读 [Experience Platform概述](home.md).

## 主屏幕

登录Adobe Experience Platform后，您将在 [!UICONTROL 主页] 页面，由 [量度仪表板](#metrics), [近期数据](#recent-data)和 [推荐学习](#recommended-learning) 中。

![](images/user-guide/homepage.png)

### 量度

量度功能板提供了信息卡，用于提供有关您组织内的数据集、用户档案、区段和目标的信息。

![](images/user-guide/homepage-dashboard.png)

的 **[!UICONTROL 数据集]** 部分显示IMS组织内的数据集数。 此数字会在创建新数据集时更新。 有关数据集的更多信息，请参阅 [数据集概述](../catalog/datasets/overview.md).

的 **[!UICONTROL 用户档案]** 部分显示IMS组织内具有用户档案的总人数，不包括用户档案片段。 此总人数表示可寻址受众总数，每24小时更新一次。 有关用户档案的更多信息，请参阅 [实时客户资料概述](../profile/home.md).

的 **[!UICONTROL 区段]** 部分显示在IMS组织内创建的区段总数。 此数字会在创建新区段时更新。 有关区段的更多信息，请参阅 [Segmentation Service概述](../segmentation/home.md).

的 **[!UICONTROL 目标]** 部分显示为IMS组织创建的目标总数。 此数字将在创建新目标时更新。 有关目标的更多信息，请参阅 [目标概述](../destinations/home.md).

### 近期数据

最近的数据功能板提供有关最近创建的数据集、源、区段和目标的信息。

![](images/user-guide/homepage-recent.png)

的 **[!UICONTROL 最近的数据集]** 部分列出了IMS组织内最近创建的五个数据集。 每次创建新数据集时，此列表都会更新。 您可以从列表中选择一个数据集，以查看有关指定数据集的更多信息或选择 **[!UICONTROL 查看全部]** 以查看所有创建数据集的列表。 有关数据集的更多信息，请参阅 [数据集概述](../catalog/datasets/overview.md).

的 **[!UICONTROL 最近来源]** 部分列出了IMS组织内最近创建的五个源连接器。 每次创建新源连接器时，此列表都会更新。 您可以从列表中选择源连接，以查看有关指定连接器的详细信息或选择 **[!UICONTROL 查看全部]** 查看所有已创建源连接的列表。 有关源的详细信息，请参阅 [源概述](../sources/home.md).

的 **[!UICONTROL 近期区段]** 部分列出了IMS组织中最近创建的五个区段定义。 每次创建新区段定义时，此列表都会更新。 您可以从列表中选择区段定义，以查看有关指定区段定义的详细信息，或选择 **[!UICONTROL 查看全部]** 以查看所有创建的区段定义的列表。 有关区段的更多信息，请参阅 [Segmentation Service概述](../segmentation/home.md).

的 **[!UICONTROL 近期目标]** 部分列出了IMS组织内最近创建的五个目标。 每次创建新目标时，此列表都会更新。 您可以从列表中选择一个目标，以查看有关指定目标的更多信息，或选择 **[!UICONTROL 查看全部]** 以查看所有已创建目标的列表。 有关目标的更多信息，请参阅 [目标概述](../destinations/home.md).

### 推荐学习

的 **[!UICONTROL 推荐学习]** 部分提供了有用文档的链接，以开始使用Adobe Experience Platform。

![](images/user-guide/homepage-recommended.png)

## 顶部导航栏

Platform UI中的顶部导航栏会显示您当前已登录的IMS组织，并提供一些重要控件。

导航栏左侧是Adobe Experience Platform徽标。 随时选择此徽标将返回Platform UI主屏幕。

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS组织切换器

顶部导航栏右侧的第一个项目是 **IMS组织切换器**.

![](./images/user-guide/homepage-ims-org-switcher.png)

选择切换器会打开一个包含您有权访问的IMS组织的下拉菜单（如果有）。 要切换到其他IMS组织，请选择一个列出的选项。

### 切换应用程序

顶部导航右侧的下一个项目是 **应用程序切换器**，由 ![应用程序切换器](./images/user-guide/app-switcher-icon.png) 图标。 当您选择此图标时，您可以在IMS组织有权访问的Adobe应用程序(如Experience Platform、分析、资产等)之间切换。

### 帮助

应用程序切换器的右侧是 **帮助和支持菜单**，以 ![问号/帮助](./images/user-guide/help-icon.png) 图标。 选择此图标时，会显示一个弹出菜单，其中包含多个帮助和支持资源。 的 **[!UICONTROL 帮助]** 选项卡会显示当前所在页面的相关文档列表。 的 **[!UICONTROL 支持]** 选项卡，用于与Adobe支持团队创建支持票证。 的 **[!UICONTROL 反馈]** 选项卡，用于向Adobe提交有关Platform的反馈。

![](images/user-guide/homepage-help-clicked.png)

### 通知和公告

在 **通知部分**，以 ![钟/通知和公告](images/user-guide/notification-icon.png) 图标。 的 **[!UICONTROL 通知]** 选项卡显示有关产品和其他相关更新的重要信息，而 **[!UICONTROL 公告]** 选项卡显示有关服务维护的信息。

### 用户配置文件

顶部导航栏上的最后一项是 **用户设置**，由 ![用户设置/用户配置文件](images/user-guide/profile-icon.png) 图标。 选择此图标可编辑首选项或注销。

您可以在Platform界面的明暗主题之间进行切换，其中的开关位于您姓名和电子邮件正下方。 选择您喜欢的主题。

![](images/theme.png)

### 沙盒

沙盒栏紧靠顶部导航栏的下方。 此栏显示您当前用于Platform的沙箱。 有关沙箱的更多信息，请参阅 [沙箱概述](../sandboxes/home.md).

## 左侧导航栏 {#left-nav}

屏幕左侧的导航列出了Platform UI中支持的所有不同服务。

单击菜单图标可显示或隐藏左侧导航面板。

![](images/user-guide/hidemenu.png)

显示面板后，再次单击可锁定打开位置的导航。

>[!IMPORTANT]
>
>左侧导航栏仅显示您能够访问的功能。 在Adobe Experience Platform的早期版本中，不可用项目处于禁用状态。 如果您认为您应该有权访问未显示的部分，请联系您的系统管理员。

![](images/user-guide/homepage-left.png)

的 **[!UICONTROL 主页]** 部分，可返回到Platform UI主页。

的 **[!UICONTROL 工作流]** 部分显示用于在Platform中执行操作的多步工作流列表。 有关工作流的更多信息，请参阅 [工作流概述](./workflows.md).

### [!UICONTROL 连接]

的 **[!UICONTROL 源]** 部分允许您创建、更新和删除源连接，从而允许您将数据从外部源摄取到平台。 有关源的详细信息，请参阅 [源概述](../sources/home.md).

的 **[!UICONTROL 目标]** 部分允许您创建、更新和删除目标，从而将数据从Platform导出到许多外部目标。 有关目标的更多信息，请参阅 [目标概述](../destinations/home.md).

### [!UICONTROL 客户]

的 **[!UICONTROL 用户档案]** 通过部分，您可以浏览客户配置文件、查看配置文件量度、创建和管理合并策略以及查看合并架构。 要了解有关使用 [!UICONTROL 用户档案] 部分，请阅读 [[!DNL Profile] 用户指南](../profile/ui/user-guide.md). 有关实时客户资料的更多信息，请参阅 [实时客户资料概述](../profile/home.md).

的 **[!UICONTROL 区段]** 部分，可创建和管理区段定义。 要了解有关使用 [!UICONTROL 区段] 部分，请阅读 [分段用户指南](../segmentation/ui/overview.md). 有关Segmentation Service的更多信息，请参阅 [Segmentation Service概述](../segmentation/home.md).

的 **[!UICONTROL 标识]** 部分，可让您创建和管理身份命名空间。 有关 [!UICONTROL 标识] 部分，包括有关身份命名空间以及如何在Platform UI中使用身份的信息，请参阅 [身份命名空间概述](../identity-service/namespaces.md).

### [!UICONTROL Privacy]

的 **[!UICONTROL 策略]** 部分，可让您创建和管理数据使用策略。 要了解有关使用策略部分的更多信息，请阅读 [数据使用策略用户指南](../data-governance/policies/user-guide.md). 有关数据使用策略的更多信息，请参阅 [数据使用策略概述](../data-governance/policies/overview.md).

的 **[!UICONTROL 请求]** 部分，可让您创建和管理隐私请求。 请注意，必须列入允许列表您才能访问Privacy ServiceUI。 要了解有关使用“请求”部分的更多信息，请阅读 [Privacy Service用户指南](../privacy-service/ui/user-guide.md). 有关Privacy Service的更多信息，请参阅 [Privacy Service概述](../privacy-service/home.md).

### [!UICONTROL 数据科学]

的 **[!UICONTROL 笔记本]** JupyterLab是一个交互式开发环境，可让您探索、分析和建模数据。 要了解有关使用笔记本部分的更多信息，请阅读 [JupyterLab用户指南](../data-science-workspace/jupyterlab/overview.md). 有关数据科学工作区的更多信息，请参阅 [数据科学工作区概述](../data-science-workspace/home.md)

的 **[!UICONTROL 模型]** 部分允许您使用机器学习和人工智能来创建、开发、训练和调整模型以进行预测。 有关“模型”部分的更多信息，请参阅 [训练和评估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

的 **[!UICONTROL 服务]** 部分，您可以管理发布的模型以进行计划培训和评分，或使用Adobe的Intelligent Services（一组AI服务，可提供实时、个性化的客户体验）。 有关“服务”部分的更多信息，请参阅 [发布模型为服务教程](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL 数据管理]

的 **[!UICONTROL 模式]** 通过部分，您可以创建和管理体验数据模型(XDM)架构。 要进一步了解模式，请阅读 [创建模式](../xdm/tutorials/create-schema-ui.md). 有关XDM的更多信息，请参阅 [XDM系统概述](../xdm/home.md).

的 **[!UICONTROL 数据集]** 区域，以创建和管理数据集。 有关数据集的更多信息，请参阅 [datasets用户指南](../catalog/datasets/user-guide.md).

的 **[!UICONTROL 查询]** 部分允许您创建和管理查询、记录由Adobe Experience Platform查询服务发出的SQL查询，以及查看 [!DNL PostgreSQL] 凭据。 有关查询的更多信息，请参阅 [查询服务用户指南](../query-service/ui/overview.md).

的 **[!UICONTROL 监控]** 部分，可让您监控批量摄取和流式摄取。 有关监控的更多信息，请参阅 [监控数据摄取用户指南](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL 决策]

Adobe Journey Optimizer是一项基于Experience Platform构建的应用程序服务。 它允许您使用强大的决策技术，在适当的时间跨所有接触点为客户提供最佳选件和体验。 进一步了解Journey Optimizer，包括与 [!UICONTROL 选件] 和 [!UICONTROL 活动] 访问 [Journey Optimizer文档](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hans).

### [!UICONTROL 管理]

平台用户界面(UI)提供了一个功能板，您可以通过该功能板查看有关贵组织许可证使用情况的重要信息，这些信息是在每日快照期间捕获的。 通过选择 **[!UICONTROL 许可证使用情况]** 中。 要进一步了解许可证使用功能板，请访问 [许可证使用仪表板指南](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>许可证使用功能板功能当前位于alpha中，并非所有用户都可用。 文档和功能可能会发生变化。

## 后续步骤

通过阅读本指南，您现在已介绍到Platform UI的主页和主要导航元素。 有关在用户界面中工作的更多详细信息，请参阅每个Platform服务的相关文档。 有关此文档的链接，请参阅 [左侧导航](#left-nav) 部分。
