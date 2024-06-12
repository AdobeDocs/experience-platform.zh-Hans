---
title: 帐户配置文件仪表板
description: Adobe Experience Platform提供了一个功能板，通过该功能板可查看有关贵组织的B2B帐户配置文件的重要信息。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 8e05b0ae06250f8cd55b361a8176963e0dce8e92
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 1%

---

# [!UICONTROL 帐户配置文件] 仪表板

Adobe Experience Platform用户界面(UI)提供了一个功能板，通过该功能板，您可以查看有关帐户配置文件的重要信息，在每日快照期间捕获了这些信息。 本指南概述如何访问和使用 [!UICONTROL 帐户配置文件] 功能板，并提供有关功能板中显示的可视化的更多信息。

本文档概述了 [!UICONTROL 帐户配置文件] 功能板，并详细描述可用的标准见解。 请参阅 [[!UICONTROL 帐户配置文件] UI指南](../../rtcdp/accounts/account-profile-ui-guide.md) 以了解有关其可用功能的完整详细信息。

## 快速入门

您必须有权使用 [Adobe Real-time Customer Data Platform B2B版本](../../rtcdp/b2b-overview.md) 访问B2B [!UICONTROL 帐户配置文件] 仪表板。

## 帐户配置文件数据 {#data}

此 [!UICONTROL 帐户配置文件] 仪表板显示统一帐户信息的快照。 此帐户信息来自您的营销渠道中的多个来源，以及贵组织当前用于存储客户帐户信息的各种系统。

快照中的配置文件数据显示的数据与拍摄快照的特定时间点完全相同。 换句话说，快照不是数据的近似值或样本，而 [!UICONTROL 帐户配置文件] 仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新都不会反映在功能板中，直到拍摄下一个快照为止。

## 浏览 [!UICONTROL 帐户配置文件] 仪表板 {#explore}

要导航至 [!UICONTROL 帐户配置文件] 在Platform UI中，选择 **[!UICONTROL 配置文件]** 下 [!UICONTROL 帐户] （在左侧导航面板中）。

![左侧导航中带有帐户配置文件的Platform UI突出显示，并显示“概述”选项卡。](../images/account-profiles/account-profiles-dashboard.png)

从 [!UICONTROL 帐户配置文件] 仪表板，您可以 [浏览引入到您组织中的帐户配置文件](#browse-account-profiles)，或 [使用小组件一目了然地查看您的帐户配置文件数据的全部](#standard-widgets).

### 日期过滤器 {#date-filter}

此 [!UICONTROL 概述] 选项卡由若干小组件组成，这些小组件提供只读量度，以传达有关您的帐户配置文件的重要信息。 选择日历图标或日期以更改小组件的全局日期过滤器。

>[!IMPORTANT]
>
>您在下拉日历中选择的日期范围会影响除两个预测评分构件([分布](#predictive-scoring-distribution) 和 [主要影响因素](#predictive-scoring-top-influential-factors))。

![突出显示日期选择器和过滤器图标的帐户配置文件概述选项卡。](../images/account-profiles/date-filter.png)

### 配置潜在客户到帐户的匹配服务 {#lead-to-account-matching-service}

选择 **[!UICONTROL 设置]** 从配置潜在客户到帐户的匹配服务 [!UICONTROL 帐户设置] 对话框。 有关如何配置潜在客户与帐户匹配的完整详细信息，请参阅 [UI指南](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). 要了解有关潜在客户与帐户匹配的更多信息，请参阅 [导致Real-Time CDP B2B文档中的帐户匹配](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![突出显示设置的帐户配置文件仪表板。](../images/account-profiles/settings.png)

## 浏览帐户配置文件 {#browse-account-profiles}

从 [!UICONTROL 浏览] 选项卡，您可以搜索和查看引入到组织中的只读帐户配置文件。 使用连接的企业源中的帐户ID或直接输入源详细信息。 从该工作区中，您可以查看属于帐户配置文件的重要信息，包括其名称、行业、收入和受众等。

选择 [!UICONTROL 配置文件ID] 结果显示在 [!UICONTROL 浏览] 选项卡以打开 [!UICONTROL 详细信息] 帐户配置文件的选项卡。

![帐户配置文件浏览选项卡，其中显示了结果并突出显示配置文件ID。](../images/account-profiles/account-profiles-browse-tab.png)

显示在上的帐户配置文件信息 [!UICONTROL 详细信息] 选项卡已从多个配置文件片段合并在一起，以形成单个帐户的单个视图。 请参阅相关文档 [在Adobe Real-time Customer Data Platform中浏览帐户配置文件](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 详细了解Platform UI中的帐户个人资料查看功能。

## 标准构件 {#standard-widgets}

Adobe提供了标准构件，可用于可视化与帐户配置文件相关的各种指标。

>[!IMPORTANT]
>
>如果不提供日期过滤器，则分析的默认行为是分析从去年到今天添加的数据。

要了解有关每个可用标准构件的更多信息，请从以下列表中选择构件的名称：

* [已添加帐户轮廓](#account-profiles-added)
* [按行业划分的新客户](#accounts-by-industry)
* [按类型的新帐户](#accounts-by-type)
* [按人员角色显示的新机会](#opportunities-by-person-role)
* [按收入显示的新机会](#opportunities-by-revenue)
* [按状态和阶段显示的新机会](#opportunities-by-status-&-stage)
* [赢得新机会](#opportunities-won)
* [新增机会](#opportunities-added)
* [预测评分分布](#predictive-scoring-distribution)
* [预测得分主要影响因素](#predictive-scoring-top-influential-factors)

### 已添加帐户轮廓 {#account-profiles-added}

此 [!UICONTROL 已添加帐户配置文件] 构件使用折线图显示一段时间内每天添加的帐户配置文件数。 使用位于仪表板顶部的全局日期过滤器来确定分析时段。 如果未提供日期过滤器，则默认行为会列出为今天之前的一年添加的帐户配置文件。 结果可用于推断添加的帐户配置文件数量的趋势。

![帐户配置文件已添加构件。](../images/account-profiles/account-profiles-added.png)

### 按行业划分的新客户 {#accounts-by-industry}

此 [!UICONTROL 按行业划分的新客户] 小组件显示圆环图中单个量度的帐户总数。 圆环图说明了构成这一总额的不同行业的相对构成。 颜色编码的密钥提供所有包含行业的细目。 当光标悬停在圆环图的相应部分上时，会在对话框中显示每个行业的各个计数。

![按行业划分的新帐户。](../images/account-profiles/new-accounts-by-industry.png)

### 按类型的新帐户 {#accounts-by-type}

此 [!UICONTROL 按类型的新帐户] 小组件显示圆环图中单个量度的帐户总数。 圆环图说明了构成此总额的不同帐户类型的相对构成。 颜色编码的密钥提供所有包含的帐户类型的细分。 当光标悬停在圆环图的相应部分上时，每种类型的帐户分别显示在一个对话框中。

![按类型划分的新帐户。](../images/account-profiles/new-accounts-by-type.png)

### 按人员角色显示的新机会 {#opportunities-by-person-role}

此 [!UICONTROL 按人员角色显示的新机会] 小组件在圆环图中显示在单个量度中的机会总数。 圆环图说明了构成此机会总数的角色的相对构成。 颜色编码的密钥提供包含的所有角色的细分。 当光标悬停在圆环图的相应部分上时，将在对话框中显示每个角色的单个计数。

>[!NOTE]
>
>此 [!UICONTROL 未找到数据] 或 [!UICONTROL 无法加载] 当您的架构中未使用“Opportunity-Person”桥表时，会导致错误。 如果您的分析显示其中一个错误，请检查您的合并架构并确保“Opportunity-Person”字段组正在摄取数据。

![按人员列出的新机会角色小组件。](../images/account-profiles/new-opportunities-by-person-role.png)

### 按收入显示的新机会 {#opportunities-by-revenue}

此 [!UICONTROL 按收入显示的新机会] 构件使用条形图来说明您的机会所产生的总预计收入额。 该构件最多支持六个机会。

要查看包含opportunity的特定收入总计的对话框，请使用光标悬停在各个栏上。

![按收入显示的新机会widget.](../images/account-profiles/new-opportunities-by-revenue.png)

### 按状态和阶段显示的新机会 {#opportunities-by-status-&-stage}

此构件使用条形图来说明在营销/销售漏斗的所有阶段打开或关闭的机会数量。 构件使用颜色来区分机会的阶段。 颜色编码的键表示机会的可用阶段。

![按状态和暂存构件显示的新机会。](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### 赢得新机会 {#opportunities-won}

此 [!UICONTROL 赢得新机会] 小组件在圆环图中显示已在单个指标中成功完成的机会总数。 圆环图说明了获胜或未获胜机会的相对构成。 颜色编码密钥用于区分成功和未成功的机会。 当光标悬停在圆环图的相应部分上时，将在对话框中显示每个角色的单个计数。

![“新机遇”赢得了Widget。](../images/account-profiles/new-opportunities-won.png)

### 新增机会 {#opportunities-added}

此 [!UICONTROL 已添加机会] 构件使用线形图显示一段时间内每天添加的业务机会数量。 使用位于仪表板顶部的全局日期过滤器来确定分析时段。 如果未提供日期过滤器，则默认行为会列出为今天之前的一年添加的机会。 结果可用于推断所添加机会数的趋势。

<!-- Link to date filter documentation from Annamalai -->

![机会添加了构件。](../images/account-profiles/opportunities-added.png)

### 预测评分分布 {#predictive-scoring-distribution}

此 [!UICONTROL 预测评分分布] widget显示所有客户档案的分数分布，以帮助您一眼就了解销售渠道的运行状况。 评分数据通过圆环图和柱状图传递。

圆环图说明了您的总帐户配置文件在高、中和低购买存储桶倾向中的比例。 键提供了有关颜色编码的部分的更多详细信息，包括评分存储段范围以及该范围内的帐户配置文件数。

柱形图提供了更细粒度的评分细分。 每列显示20个五点增量分段中每个分段的帐户配置文件数。

利用小组件中的下拉菜单，可选择帐户评分模型。

>[!NOTE]
>
>全局日期范围过滤器不适用于预测评分见解。 预测评分构件根据在下拉列表中选定的帐户评分模型分析数据。

![预测评分分布构件。](../images/account-profiles/predictive-scoring-distribution.png)

### 预测得分主要影响因素 {#predictive-scoring-top-influential-factors}

此 [!UICONTROL 预测得分主要影响因素] 构件可帮助您了解促使每个倾向存储桶得分的最重要因素。

此构件显示每个高、中和低倾向存储桶的主要影响因素。 每个影响因子的栏指示该倾向区间中包含特定影响因子的帐户用户档案的百分比。

利用小组件中的下拉菜单，可选择帐户评分模型。

>[!NOTE]
>
>全局日期范围过滤器不适用于预测评分见解。 预测评分构件根据在下拉列表中选定的帐户评分模型分析数据。

![预测得分主要影响因素小组件。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

### 无法加载数据错误 {#errors}

如果显示构件 *[!UICONTROL 无法加载。 请重试。]* 这是因为没有可用于B2B实体的数据。 例如，以下显示的构件 [!UICONTROL 按人员角色显示的新机会]，显示消息“[!UICONTROL 无法加载。 请重试。]”因为该沙盒没有可用的opportunity数据。

![无法加载分析错误。](../images/account-profiles/unable-to-load.png)

要解决此问题，必须摄取B2B实体数据，例如 *机会人员* 数据，放入沙盒中。 48小时后，数据反映在小组件中。

## 后续步骤

现在，通过阅读本文档，您应该知道如何找到 [!UICONTROL 帐户配置文件] 并了解可用小组件中显示的量度。 要了解有关在Experience PlatformUI中使用作为B2B数据一部分的帐户配置文件的更多信息，请参阅 [帐户配置文件概述](../../rtcdp/accounts/account-profile-overview.md) 适用于Adobe Real-Time CDP的B2B版本。
