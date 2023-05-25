---
title: 帐户配置文件仪表板指南
description: Adobe Experience Platform提供了一个功能板，通过它可查看有关贵组织的B2B帐户配置文件的重要信息。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!UICONTROL 帐户配置文件] 仪表板

Adobe Experience Platform用户界面(UI)提供了一个功能板，通过它可查看有关帐户配置文件的重要信息，这些信息会在每日快照期间捕获。 本指南概述如何访问和使用 [!UICONTROL 帐户配置文件] 提供了有关仪表板中显示的可视化的更多信息。

要了解帐户配置文件用户界面中所有功能的概述，请访问 [帐户配置文件UI指南](../../rtcdp/accounts/account-profile-ui-guide.md).

## 快速入门

您必须有权使用 [Adobe Real-time Customer Data Platform B2B版本](../../rtcdp/b2b-overview.md) 以访问B2B [!UICONTROL 帐户配置文件] 仪表板。

## 帐户配置文件数据

此 [!UICONTROL 帐户配置文件] 功能板显示来自营销渠道的多个来源以及您的组织当前用于存储客户帐户信息的各种系统的统一帐户信息的快照。

快照中的配置文件数据显示的数据与拍摄快照时特定时间点显示的数据完全相同。 换句话说，快照不是数据的近似值或样本，而 [!UICONTROL 帐户配置文件] 仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新都不会反映在功能板中，直到拍摄下一个快照为止。

## 探索 [!UICONTROL 帐户配置文件] 仪表板

要导航到 [!UICONTROL 帐户配置文件] 在Platform UI中，选择 **[!UICONTROL 配置文件]** 下 [!UICONTROL 帐户] 左侧导航面板中。

![左侧导航中带有帐户配置文件的Platform UI突出显示，并显示“概述”选项卡。](../images/account-profiles/account-profiles-dashboard.png)

从 [!UICONTROL 帐户配置文件] 功能板，您可以 [浏览引入到您组织中的帐户配置文件](#browse-account-profiles)，或 [使用小组件一目了然地查看所有帐户配置文件数据](#standard-widgets) 可将数据的各个方面进行可视化。

## 浏览帐户配置文件 {#browse-account-profiles}

此 [!UICONTROL 浏览] 选项卡允许您搜索并查看只读帐户配置文件，这些配置文件是使用来自连接的企业源的帐户ID或通过直接输入源详细信息引入贵组织的。 从这里，您可以看到属于客户档案的重要信息，包括其名称、行业、收入和区段等。

选择 [!UICONTROL 配置文件ID] 结果显示在 [!UICONTROL 浏览] 选项卡以打开 [!UICONTROL 详细信息] 帐户配置文件的选项卡。

![Account Profiles browse选项卡中显示了结果，并突出显示了Profile ID。](../images/account-profiles/account-profiles-browse-tab.png)

显示在上的帐户配置文件信息 [!UICONTROL 详细信息] 选项卡已从多个配置文件片段合并在一起，以形成单个帐户的单个视图。 请参阅相关文档 [在Adobe Real-time Customer Data Platform中浏览帐户配置文件](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 详细了解Platform UI中的帐户配置文件查看功能。

## 此 [!UICONTROL 帐户配置文件] [!UICONTROL 概述] {#overview}

此 [!UICONTROL 概述] 选项卡由小组件组成，这些小组件提供只读量度，以传达有关您的帐户配置文件的重要信息。 选择 **[!UICONTROL 修改仪表板]** 以更改 [!UICONTROL 概述] 通过移动小部件和调整其大小来制表符。

![突出显示“修改”功能板的“帐户配置文件概述”选项卡。](../images/account-profiles/modify-dashboard.png)

请参考以下文档： [修改仪表板](../customize/modify.md) 和 [构件库概述](../customize/widget-library.md) 了解更多信息。

## 标准构件 {#standard-widgets}

Adobe提供了标准构件，可用于可视化与帐户配置文件相关的各种指标。

要详细了解每个可用的标准构件，请从以下列表中选择构件的名称：

* [按行业划分的帐户总数](#total-accounts-by-industry)
* [已添加帐户配置文件](#account-profiles-added)
* [预测评分分布](#predictive-scoring-distribution)
* [预测评分主要影响因素](#predictive-scoring-top-influential-factors)

### 按行业划分的帐户总数 {#total-accounts-by-industry}

此小部件显示单个指标中的帐户总数，并使用圆环图说明构成总数的行业中计数的比例大小。 键值为构成圆环图的不同行业提供颜色编码信息。

当光标悬停在圆环图的相应部分上时，不同行业的单个计数显示在对话框中。

![按行业构件划分的总帐户数。](../images/account-profiles/total-accounts-by-industry-widget.png)

### 已添加帐户配置文件 {#account-profiles-added}

此构件使用颜色编码的条形图来说明在给定时间段内添加到帐户的用户档案计数，以及构成这些添加的用户档案的不同行业比例。 各行业采用颜色编码，一个键为构成条形图的不同行业提供颜色编码信息。 从小组件下拉菜单中选择分析时段。 条形图可以在30天、90天和12个月的时段内可视化。

>[!NOTE]
>
>由于配置文件仅添加到帐户且永远不会删除，因此在一段时间内添加的最少配置文件数为零。

![帐户配置文件已添加构件。](../images/account-profiles/accounts-profiles-added-widget.png)

### 预测评分分布 {#predictive-scoring-distribution}

此 [!UICONTROL 预测评分分布] widget显示所有客户档案的分数分布，以帮助您一目了然地了解销售管道的运行状况。 评分数据通过圆环图和柱状图传递。

圆环图说明了您的总客户档案在高、中、低购买倾向各时段中的比例。 键提供了有关颜色编码的部分的更多详细信息，包括评分存储段范围以及该范围内的帐户配置文件数。

柱状图提供了更细粒度的评分细分。 每列显示20个五点增量存储桶中每个存储桶中的帐户配置文件数。

利用小组件中的下拉菜单，可选择帐户评分模型。

![预测评分分布构件。](../images/account-profiles/predictive-scoring-distribution.png)

### 预测评分主要影响因素 {#predictive-scoring-top-influential-factors}

此 [!UICONTROL 预测评分主要影响因素] 构件可帮助您了解驱动每个倾向存储桶得分的最重要因素。

此构件显示每个高、中和低倾向存储桶的主要影响因素。 每个影响因素的栏表示该倾向区间中包含特定影响因素的帐户用户档案的百分比。

利用小组件中的下拉菜单，可选择帐户评分模型。

![预测评分主要影响因素小组件。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 后续步骤

现在，通过阅读本文档，您应该知道如何找到 [!UICONTROL 帐户配置文件] 仪表板。 您还应了解可用构件中显示的量度。 要了解有关在Experience PlatformUI中将帐户配置文件用作B2B数据一部分的更多信息，请参阅 [帐户配置文件概述](../../rtcdp/accounts/account-profile-overview.md) 适用于Adobe Real-Time CDP的B2B版本。
