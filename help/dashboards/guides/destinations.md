---
keywords: Experience Platform；配置文件；实时客户配置文件；用户界面；UI；自定义；配置文件功能板；功能板
title: 目标功能板
description: Adobe Experience Platform提供了一个功能板，您可以通过该功能板查看有关贵组织活动目标的重要信息。
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 65096a2da03f504c16f00a75bfdef9e78f8c1799
workflow-type: tm+mt
source-wordcount: '2538'
ht-degree: 0%

---

# [!UICONTROL 目标] 仪表板

Adobe Experience Platform用户界面(UI)提供了一个功能板，您可以通过该功能板查看有关贵组织活动目标的重要信息，这些信息是在每日快照期间捕获的。 本指南概述了如何在UI中访问和使用目标功能板，并提供了有关功能板中显示的量度的更多信息。

有关目标的概述以及Experience Platform中所有可用目标的目录，请访问 [目标文档](../../destinations/home.md).

## [!UICONTROL 目标] 仪表板数据 {#destinations-dashboard-data}

的 [!UICONTROL 目标] 功能板显示贵组织在Experience Platform中启用的目标快照。 快照中的数据与拍摄快照时在特定时间点显示的数据完全一样。 换句话说，快照不是数据的近似值或样本，目标仪表板也不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新，在拍摄下一个快照之前不会反映在功能板中。

## 浏览目标仪表板

要导航到Platform UI中的目标功能板，请选择 **[!UICONTROL 目标]** 在左边栏中，选择 **[!UICONTROL 概述]** 选项卡来显示功能板。

>[!NOTE]
>
>如果贵组织是新Experience Platform，并且还没有活动目标，则 [!UICONTROL 目标] 功能板和 [!UICONTROL 概述] 选项卡。 而是选择 [!UICONTROL 目标] 在左侧导航中， [!UICONTROL 目录] 选项卡。 要进一步了解 [!UICONTROL 目录] 选项卡，请参阅 [[!UICONTROL 目标] 工作区指南](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### 修改目标功能板

您可以通过选择 **[!UICONTROL 修改功能板]**. 这样，您就可以在功能板中移动、添加和删除小组件，以及访问 **[!UICONTROL 构件库]** 以浏览可用小组件并为贵组织创建自定义小组件。

请参阅 [修改功能板](../customize/modify.md) 和 [构件库概述](../customize/widget-library.md) 文档以了解更多信息。

## 标准小组件

Adobe提供了多个标准小组件，您可以使用这些小组件来可视化与您的目标相关的不同量度，并评估可用于数据分析的区段的完整性。 您还可以使用 [!UICONTROL 构件库]. 要了解有关创建自定义小组件的更多信息，请首先阅读 [构件库概述](../customize/widget-library.md).

要进一步了解每个可用的标准小组件，请从以下列表中选择小组件的名称：

* [[!UICONTROL 最常用的目标]](#most-used-destinations)
* [[!UICONTROL 最近创建的目标]](#recently-created-destinations)
* [[!UICONTROL 最近激活的区段]](#recently-activated-segments)
* [[!UICONTROL 最近激活的区段（按目标）]](#recently-activated-segments-by-destination)
* [[!UICONTROL 受众大小趋势]](#audience-size-trend)
* [[!UICONTROL 按身份划分的未映射区段]](#unmapped-segments-by-identity)
* [[!UICONTROL 按身份映射的区段]](#mapped-segments-by-identity)
* [[!UICONTROL 常见受众]](#common-audiences)
* [[!UICONTROL 映射的受众运行状况]](#mapped-audience-health)
* [[!UICONTROL 目标计数]](#destinations-count)
* [[!UICONTROL 目标状态]](#destination-status)
* [[!UICONTROL 按目标平台划分的活动目标]](#active-destinations-by-destination-platform)
* [[!UICONTROL 所有目标中的已激活受众]](#activated-audiences-across-all-destinations)

### [!UICONTROL 最常用的目标] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="最常用的目标"
>abstract="此小组件按映射的区段数量显示贵组织最活跃的目标。 这些数字在上次快照时是准确的。 此排名可深入分析当前最常使用的目标，同时突出显示可能未充分利用的目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#most-used-destinations" text="从文档了解更多信息"

的 **[!UICONTROL 最常用的目标]** 小组件按映射的区段数显示自上次快照起您组织的热门目标。 此排名提供了有关哪些目标正在被利用的洞察信息，同时还可能显示那些可能未充分利用的目标。

例如，如果您昨天配置了一个目标，但尚未将任何区段映射到该目标，则您将能够看到该目标当前未充分利用。

截至上次每日快照时，区段计数列中显示的已映射区段数是准确的。 将新区段映射到目标将不会更新计数，直到拍摄下一个快照。

从小组件上显示的列表中选择目标名称后，您将转到 **[!UICONTROL 浏览]** 选项卡。 您还可以选择 **[!UICONTROL 查看全部]** 导航到 **[!UICONTROL 浏览]** 选项卡，然后选择目标的名称以查看其详细信息。

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近创建的目标] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="最近创建的目标"
>abstract="此小组件会显示您组织内最近配置的目标列表。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#recently-created-destinations" text="从文档了解更多信息"

的 **[!UICONTROL 最近创建的目标]** 小组件允许您查看组织最近配置的目标列表。

显示的创建日期精确到最后的每日快照。 换言之，如果您创建了新目标，则在拍摄下一个快照之后，该目标才会显示在列表中。

从小组件上显示的列表中选择目标名称后，您将转到 **[!UICONTROL 浏览]** 选项卡。 您还可以选择 **[!UICONTROL 查看全部]** 导航到 **[!UICONTROL 浏览]** 选项卡，然后选择目标的名称以查看其详细信息。

要进一步了解如何配置特定类型的目标，请访问 [目标文档](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近激活的区段] {#recently-activated-segments}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="最近激活的区段"
>abstract="此小组件提供最近映射到目标的区段列表。 此列表提供了系统中正在使用的区段和目标的快照，并有助于对任何错误映射进行故障诊断。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#recently-activated-segments" text="从文档了解更多信息"

的 **[!UICONTROL 最近激活的区段]** 小组件提供了最近映射到目标的区段列表。 此列表提供了系统中正在使用的区段和目标的快照，并有助于对任何错误映射进行故障诊断。

显示的更新日期显示区段上次激活到目标的时间，并准确到最后的每日快照。 换句话说，如果您将区段激活到目标，则更新日期在拍摄下一个快照之后才会更改。

从小组件上显示的列表中选择区段名称后，您将转到区段详细信息。 您还可以选择 **[!UICONTROL 查看全部]** 导航到区段浏览选项卡，然后选择区段名称以查看其详细信息。

有关在Experience Platform中使用区段的更多信息，请首先阅读 [Segmentation Service概述](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

### [!UICONTROL 最近激活的区段（按目标）] {#recently-activated-segments-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="最近激活的区段（按目标）"
>abstract="此小组件会根据概述下拉菜单中选择的目标，以降序方式显示前五个最近激活的区段。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#recently-activated-segments-by-destination" text="从文档了解更多信息"

的 **[!UICONTROL 最近激活的区段（按目标）]** 小组件会根据概述下拉列表中选择的目标，以降序方式显示前五个最近激活的区段。 它类似于 [!UICONTROL 最近激活的区段] 小组件，但显示的数据 **仅** 应用到所选目标。

此小组件包含两个量度：区段名称以及区段上次激活到目标的日期。 显示的数据自上次每日快照开始是正确的。

您可以通过从显示的列表中选择区段名称来查看区段的详细信息。

![最近由目标小组件激活的区段。](../images/destinations/recently-activated-segments-by-destination.png)

### [!UICONTROL 受众大小趋势] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="受众大小趋势"
>abstract="此小组件说明区段中包含的每天发送到目标帐户的用户档案数。 第一个下拉菜单调整受众趋势的时间段。 第二个小组件下拉菜单选择要分析的区段。 从概述下拉菜单中选择了目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#audience-size-trend" text="从文档了解更多信息"

的 **[!UICONTROL 受众大小趋势]** 小组件描述了已映射到该目标帐户的区段在一段时间内的配置文件计数关系。 小组件使用折线图来说明区段中包含的每天发送到目标帐户的用户档案数。

过去30天、90天或12个月内受众趋势的时间段，可以使用第一个下拉菜单进行调整。

第二个下拉菜单列出了每个可用区段，这些区段可发送到功能板顶部选择的目标帐户。

![受众大小趋势小组件。](../images/destinations/audience-size-trend.png)

的 **[!UICONTROL 受众大小趋势]** 小组件提供 [!UICONTROL 字幕] 按钮。 选择 **[!UICONTROL 字幕]** 打开自动字幕对话框。 机器学习模型通过分析图表和区段数据自动生成字幕以描述关键趋势和重要事件。

![受众大小趋势小组件的自动字幕对话框。](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL 按身份划分的未映射区段] {#unmapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="按身份划分的未映射区段"
>abstract="此小组件列出了前5个 **未映射** 按给定目标和身份的降序身份计数排名的区段。 小组件下拉列表中列出的过滤器ID会因在概述页面顶部选择的目标帐户而发生更改。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#unmapped-segments-by-identity" text="从文档了解更多信息"

的 **[!UICONTROL 按身份划分的未映射区段]** 小组件列出了前5个 **未映射** 按给定目标和身份的降序身份计数排名的区段。 它会突出显示根据所选ID映射到所选目标帐户最有用的区段。

目标ID下拉列表可过滤您的可用区段。 下拉列表中列出的过滤器ID会因在概述页面顶部选择的目标帐户而发生更改。

标识列计算区段内可映射到小组件ID下拉列表中所选ID的源ID数量。

![按身份小组件显示的未映射区段。](../images/destinations/unmapped-segments-by-identity.png)

### [!UICONTROL 按身份映射的区段] {#mapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="按身份映射的区段"
>abstract="此小组件提供了 **映射** 区段。 根据区段中包含的源ID数量，列表按从高到低的顺序排列。 将从小组件标题下方的下拉菜单中选择要计数的目标ID。 小组件下拉列表中提供的目标ID取决于概述功能板顶部选择的目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#mapped-segments-by-identity" text="从文档了解更多信息"

此小组件提供了 **映射** 区段。 根据区段中包含的源ID数量，列表按从高到低的顺序排列。 将从小组件标题下方的下拉菜单中选择要计数的目标ID。 小组件中下拉列表中提供的目标ID将根据概述功能板顶部选择的目标帐户过滤器进行更改。

![按身份小组件映射的区段。](../images/destinations/mapped-segments-by-identity.png)

的 **[!UICONTROL 按身份映射的区段]** 小组件重点介绍在选定目标内成功定位营销活动用户档案机会的可能性。 有效的目标营销活动不取决于发送到目标的用户档案数量，而是取决于可能与目标ID匹配以提供有用且可操作的数据的源ID数量。

### 常见受众 {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="常见受众"
>abstract="此小组件提供了在页面顶部选择的目标帐户中激活的前五个区段的列表，以及在小组件下拉菜单中选择的目标。 区段列表会根据区段最近激活的时间进行排序。 最近激活的区段显示在顶部。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#common-audiences" text="从文档了解更多信息"

的 **[!UICONTROL 常见受众]** 小组件提供了在页面顶部选择的目标帐户中激活的前五个区段的列表，以及在小组件下拉菜单中选择的目标。 区段列表会根据区段最近激活的时间进行排序。 最近激活的区段显示在顶部。

的 [!UICONTROL 受众大小] 列提供每个列出区段的配置文件总数。

![常见受众小组件。](../images/destinations/common-audiences.png)

### 映射的受众运行状况 {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="映射的受众运行状况"
>abstract="此小组件提供了多达20个已映射区段的列表，这些区段的总配置文件计数与映射到该目标的30天平均受众大小之间至少有一个标准偏差的因子。 它提供了一个计算量度，用于衡量过去30天内受众规模与平均数的差异。 受众大小按从高到低的顺序进行排序。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#mapped-audience-health" text="从文档了解更多信息"

小组件提供了多达20个已映射区段的列表，从上次每日快照开始，这些区段的总配置文件计数与映射到该目标的30天平均受众大小之间至少有一个标准偏差的因子。

简而言之，它提供了一个计算量度，用于衡量过去30天内受众规模与平均值之间的差异。 它会比较今天的受众规模是否超出了过去30天数据中出现的历史标准差。

系统中的所有受众大小都按从高到低的受众大小进行排序，如 [!UICONTROL 最新大小] 列。

如果区段映射的配置文件计数与过去30天的平均映射配置文件大小之间的标准偏差不大，则表示系统中存在异常，应对此进行调查。

如果 [!UICONTROL 映射的受众运行状况] 小组件存在较大偏差，您应参考受众大小趋势图并查找异常区段。 该趋势可以进一步分析区段的运行状况。

![映射的受众健康小组件。](../images/destinations/mapped-audience-health.png)

### [!UICONTROL 目标计数] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="目标计数"
>abstract="此小组件提供了可在系统中激活和交付受众的可用端点总数。 此数字包括活动和不活动目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#destinations-count" text="从文档了解更多信息"

的 [!UICONTROL 目标计数] 小组件提供了可在系统中激活和交付受众的可用端点总数。 此数字包括活动和不活动目标。

在总计数以下，选择 **[!UICONTROL 目标]** 导航到目标浏览选项卡。 此页面列出了迄今为止您已与建立连接的所有目标。

![目标计数小组件。](../images/destinations/destinations-count.png)

### [!UICONTROL 目标状态] {#destination-status}

的 [!UICONTROL 目标状态] 小组件将已启用目标的总数显示为单个量度，并使用圆环图来说明已启用和已禁用目标之间的比例差异。

当光标悬停在圆环图的相应部分上时，对话框中会显示已启用或已禁用目标的单个计数。

![目标状态小组件。](../images/destinations/destination-status.png)

### [!UICONTROL 按目标平台划分的活动目标] {#active-destinations-by-destination-platform}

小组件提供了一个两列表，用于显示活动目标平台的列表以及每个目标平台的活动目标总数。 目标平台列表按从高到低的顺序排列。

![按目标平台小组件列出的活动目标。](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL 所有目标中的已激活受众] {#activated-audiences-across-all-destinations}

的 [!UICONTROL 所有目标中的已激活受众] 小组件在一个量度中提供所有目标中激活的受众总数。 此数字对于最近的快照是准确的。

![所有目标小组件中的已激活受众。](../images/destinations/activated-audiences-across-all-destinations.png)

选择 **[!UICONTROL 受众]** 导航到目标 [!UICONTROL 浏览] 选项卡。 此页面提供了所有已启用的目标和各种相关量度的列表。 请参阅相关文档 [有关 [!UICONTROL 浏览] 选项卡](../../destinations/ui/destinations-workspace.md#browse).

## 后续步骤

通过阅读本文档，您现在应该能够找到目标功能板并了解可用小组件中显示的量度。 要了解有关在Experience Platform中使用目标的更多信息，请参阅 [目标文档](../../destinations/home.md).
