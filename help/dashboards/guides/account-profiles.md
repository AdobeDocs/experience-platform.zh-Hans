---
title: 帐户配置文件功能板
description: Adobe Experience Platform提供了一个功能板，您可以通过该功能板查看有关贵组织B2B帐户配置文件的重要信息。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 8de94d38fd1d2c001935180851d6877dfe2a8941
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---

# [!UICONTROL 帐户配置文件] 仪表板

Adobe Experience Platform用户界面(UI)提供了一个功能板，通过该功能板可以查看有关帐户配置文件的重要信息，这些信息是在每日快照期间捕获的。 本指南概述了如何访问和使用 [!UICONTROL 帐户配置文件] 功能板，并提供有关功能板中显示的可视化的更多信息。

有关帐户用户档案用户界面中所有功能的概述，请访问 [帐户配置文件UI指南](../../rtcdp/accounts/account-profile-ui-guide.md).

## 快速入门

您必须有权 [Real-time Customer Data Platform B2B版](../../rtcdp/b2b-overview.md) 以访问B2B [!UICONTROL 帐户配置文件] 功能板。

## 帐户配置文件数据

的 [!UICONTROL 帐户配置文件] 功能板显示来自营销渠道中多个来源以及贵组织当前用于存储客户帐户信息的各种系统的统一帐户信息快照。

快照中的配置文件数据与拍摄快照时在特定时间点显示的数据完全一样。 换句话说，快照不是数据的近似值或样本， [!UICONTROL 帐户配置文件] 功能板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新，在拍摄下一个快照之前不会反映在功能板中。

## 浏览 [!UICONTROL 帐户配置文件] 仪表板

导航到 [!UICONTROL 帐户配置文件] 功能板中，选择 **[!UICONTROL 用户档案]** 在 [!UICONTROL 帐户] 中。

![左侧导航中突出显示了“帐户配置文件”的Platform UI，并显示了“概述”选项卡。](../images/account-profiles/account-profiles-dashboard.png)

从 [!UICONTROL 帐户配置文件] 功能板 [浏览摄取到您组织的帐户配置文件](#browse-account-profiles)或 [使用小组件快速查看您的帐户配置文件数据的整个](#standard-widgets) 可视化数据的各个方面。

## 浏览帐户配置文件 {#browse-account-profiles}

的 [!UICONTROL 浏览] 选项卡允许您使用从连接的企业源中的帐户ID或直接输入源详细信息来搜索和查看摄取到您组织的只读帐户配置文件。 从此处，您可以看到属于帐户配置文件的重要信息，包括其名称、行业、收入和区段等。

选择 [!UICONTROL 配置文件ID] 从 [!UICONTROL 浏览] 选项卡 [!UICONTROL 详细信息] 选项卡。

![显示结果的“帐户配置文件”浏览选项卡突出显示了配置文件ID。](../images/account-profiles/account-profiles-browse-tab.png)

在 [!UICONTROL 详细信息] 选项卡已从多个配置文件片段合并到一起，以形成单个帐户的单个视图。 请参阅 [浏览Real-time Customer Data Platform的帐户配置文件](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 要详细了解Platform UI中帐户配置文件查看功能。

## 的 [!UICONTROL 帐户配置文件] [!UICONTROL 概述] {#overview}

的 [!UICONTROL 概述] 选项卡由小组件组成，小组件提供只读量度以传递有关帐户配置文件的重要信息。 选择 **[!UICONTROL 修改功能板]** 更改 [!UICONTROL 概述] 来访问Advertising Cloud帮助。

![“帐户配置文件”概述选项卡，其中突出显示了“修改”功能板。](../images/account-profiles/modify-dashboard.png)

请参阅 [修改功能板](../customize/modify.md) 和 [构件库概述](../customize/widget-library.md) 以了解更多。

## 标准小组件 {#standard-widgets}

Adobe提供了可用于显示与帐户配置文件相关的不同量度的标准小组件。

要进一步了解每个可用的标准小组件，请从以下列表中选择小组件的名称：

* [按行业开列的帐户总数](#total-accounts-by-industry)
* [添加了帐户配置文件](#account-profiles-added)

### 按行业开列的帐户总数 {#total-accounts-by-industry}

此小组件以单个量度显示帐户总数，并使用圆环图来说明构成整体数量的行业的计数比例大小。 键可为构成圆环图的不同行业提供颜色编码信息。

当光标悬停在圆环图的相应部分上时，不同行业的单个计数将显示在对话框中。

![按行业小组件划分的帐户总数。](../images/account-profiles/total-accounts-by-industry-widget.png)

### 添加了帐户配置文件 {#account-profiles-added}

此小组件使用颜色编码条形图来说明在给定时间段内添加到帐户的用户档案计数，以及构成这些添加用户档案的不同行业的比例。 行业采用颜色编码，并且键值为构成条形图的不同行业提供颜色编码信息。 从小组件下拉菜单中选择分析周期。 条形图可在30天、90天和12个月期间进行可视化。

>[!NOTE]
>
>由于用户档案仅添加到帐户且从不删除，因此在一段时间内添加的用户档案数量最少为0。

![帐户配置文件添加了小组件。](../images/account-profiles/accounts-profiles-added-widget.png)

## 后续步骤

通过遵循本文档，您现在应该能够找到 [!UICONTROL 帐户配置文件] 功能板。 您还应了解可用小组件中显示的量度。 要了解有关在Experience PlatformUI中将帐户配置文件用作B2B数据一部分的更多信息，请参阅 [帐户配置文件概述](../../rtcdp/accounts/account-profile-overview.md) Adobe Real-Time CDP版。
