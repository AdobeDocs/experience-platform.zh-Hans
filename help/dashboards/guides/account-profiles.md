---
title: 帐户配置文件仪表板指南
description: Adobe Experience Platform提供了一个功能板，通过该功能板可查看有关贵组织的B2B帐户配置文件的重要信息。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!UICONTROL 帐户配置文件] 仪表板

Adobe Experience Platform用户界面(UI)提供了一个功能板，通过该功能板，您可以查看有关帐户配置文件的重要信息，在每日快照期间捕获了这些信息。 本指南概述如何访问和使用 [!UICONTROL 帐户配置文件] 功能板，并提供有关功能板中显示的可视化的更多信息。

欲知帐户资料用户界面中所有功能的概述，请访问 [帐户配置文件UI指南](../../rtcdp/accounts/account-profile-ui-guide.md).

## 快速入门

您必须有权使用 [Adobe Real-time Customer Data Platform B2B版本](../../rtcdp/b2b-overview.md) 以访问B2B [!UICONTROL 帐户配置文件] 仪表板。

## 帐户配置文件数据

此 [!UICONTROL 帐户配置文件] 功能板可显示来自营销渠道中的多个来源以及贵组织当前用于存储客户帐户信息的各种系统的统一帐户信息的快照。

快照中的配置文件数据显示的数据与拍摄快照的特定时间点完全相同。 换句话说，快照不是数据的近似值或样本，而 [!UICONTROL 帐户配置文件] 仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新都不会反映在功能板中，直到拍摄下一个快照为止。

## 浏览 [!UICONTROL 帐户配置文件] 仪表板

要导航至 [!UICONTROL 帐户配置文件] 在Platform UI中，选择 **[!UICONTROL 配置文件]** 下 [!UICONTROL 帐户] （在左侧导航面板中）。

![左侧导航中带有帐户配置文件的Platform UI突出显示，并显示“概述”选项卡。](../images/account-profiles/account-profiles-dashboard.png)

从 [!UICONTROL 帐户配置文件] 仪表板您可以 [浏览引入到您组织中的帐户配置文件](#browse-account-profiles)，或 [使用小组件一目了然地查看您的帐户配置文件数据的全部](#standard-widgets) 以可视化数据的各个方面。

## 浏览帐户配置文件 {#browse-account-profiles}

此 [!UICONTROL 浏览] 选项卡允许您搜索和查看使用来自连接的企业源的帐户ID或通过直接输入源详细信息摄取到您组织中的只读帐户配置文件。 从此处，您可以看到属于帐户配置文件的重要信息，包括其名称、行业、收入和受众等。

选择 [!UICONTROL 配置文件ID] 结果显示在 [!UICONTROL 浏览] 选项卡以打开 [!UICONTROL 详细信息] 帐户配置文件的选项卡。

![帐户配置文件浏览选项卡，其中显示了结果并突出显示配置文件ID。](../images/account-profiles/account-profiles-browse-tab.png)

显示在上的帐户配置文件信息 [!UICONTROL 详细信息] 选项卡已从多个配置文件片段合并在一起，以形成单个帐户的单个视图。 请参阅相关文档 [在Adobe Real-time Customer Data Platform中浏览帐户配置文件](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 详细了解Platform UI中的帐户个人资料查看功能。

## 此 [!UICONTROL 帐户配置文件] [!UICONTROL 概述] {#overview}

此 [!UICONTROL 概述] 选项卡由若干小组件组成，这些小组件提供只读量度，以传达有关您的帐户配置文件的重要信息。 选择 **[!UICONTROL 修改仪表板]** 更改 [!UICONTROL 概述] 通过移动和调整小组件大小来制表。

![突出显示修改功能板的帐户配置文件概述选项卡。](../images/account-profiles/modify-dashboard.png)

请参阅文档，网址为 [修改仪表板](../customize/modify.md) 和 [构件库概述](../customize/widget-library.md) 了解更多信息。

## 标准构件 {#standard-widgets}

Adobe提供了标准构件，可用于可视化与帐户配置文件相关的各种指标。

要了解有关每个可用标准构件的更多信息，请从以下列表中选择构件的名称：

* [按行业划分的总账户数](#total-accounts-by-industry)
* [已添加帐户配置文件](#account-profiles-added)
* [预测评分分布](#predictive-scoring-distribution)
* [预测得分主要影响因素](#predictive-scoring-top-influential-factors)

### 按行业划分的总账户数 {#total-accounts-by-industry}

此构件显示单个指标中的帐户总数，并使用圆环图说明构成总数的行业中计数的比例大小。 键值为构成圆环图的不同行业提供颜色编码信息。

当光标悬停在圆环图的相应部分上时，会在对话框中显示不同行业的各个计数。

![按行业构件划分的总帐户数。](../images/account-profiles/total-accounts-by-industry-widget.png)

### 已添加帐户配置文件 {#account-profiles-added}

此构件使用颜色编码的条形图来说明在给定时间段内添加到帐户的用户档案计数，以及构成这些添加的用户档案的不同行业比例。 各行业采用颜色编码，一个键为构成条形图的各个行业提供颜色编码信息。 从小组件下拉菜单中选择分析时段。 条形图可以在30天、90天和12个月的时段内可视化。

>[!NOTE]
>
>由于用户档案只会添加到帐户中，而不会被删除，因此在一段时间内添加的用户档案可能达到的最低数量为零。

![帐户配置文件已添加构件。](../images/account-profiles/accounts-profiles-added-widget.png)

### 预测评分分布 {#predictive-scoring-distribution}

此 [!UICONTROL 预测评分分布] widget显示所有客户档案的分数分布，以帮助您一眼就了解销售渠道的运行状况。 评分数据通过圆环图和柱状图传递。

圆环图说明了您的总帐户配置文件在高、中和低购买存储桶倾向中的比例。 键提供了有关颜色编码的部分的更多详细信息，包括评分存储段范围以及该范围内的帐户配置文件数。

柱形图提供了更细粒度的评分细分。 每列显示20个五点增量分段中每个分段的帐户配置文件数。

利用小组件中的下拉菜单，可选择帐户评分模型。

![预测评分分布构件。](../images/account-profiles/predictive-scoring-distribution.png)

### 预测得分主要影响因素 {#predictive-scoring-top-influential-factors}

此 [!UICONTROL 预测得分主要影响因素] 构件可帮助您了解促使每个倾向存储桶得分的最重要因素。

此构件显示每个高、中和低倾向存储桶的主要影响因素。 每个影响因子的栏指示该倾向区间中包含特定影响因子的帐户用户档案的百分比。

利用小组件中的下拉菜单，可选择帐户评分模型。

![预测得分主要影响因素小组件。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 后续步骤

现在，通过阅读本文档，您应该知道如何找到 [!UICONTROL 帐户配置文件] 仪表板。 您还应该了解可用构件中显示的量度。 要了解有关在Experience PlatformUI中使用作为B2B数据一部分的帐户配置文件的更多信息，请参阅 [帐户配置文件概述](../../rtcdp/accounts/account-profile-overview.md) 适用于Adobe Real-Time CDP的B2B版本。
