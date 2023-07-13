---
keywords: Experience Platform；配置文件；实时客户配置文件；用户界面；UI；自定义；配置文件仪表板；仪表板
title: 目标仪表板指南
description: Adobe Experience Platform提供了一个功能板，通过它可查看有关贵组织的活动目标的重要信息。
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 8%

---

# [!UICONTROL 目标] 仪表板

Adobe Experience Platform用户界面(UI)提供了一个功能板，通过它可查看有关贵组织的活动目标的重要信息，如在每日快照期间捕获的信息。 本指南概述如何在UI中访问和使用目标仪表板，并提供有关仪表板中显示的量度的更多信息。

有关目标的概述以及Experience Platform中所有可用目标的目录，请访问 [目标文档](../../destinations/home.md).

## [!UICONTROL 目标] 仪表板数据 {#destinations-dashboard-data}

目标仪表板显示贵组织在Experience Platform中启用的目标快照。 快照中的数据显示的数据与拍摄快照时特定时间点显示的数据完全相同。 换句话说，快照不是数据的近似值或示例，并且目标仪表板没有实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新都不会反映在功能板中，直到拍摄下一个快照为止。

## 探索 [!UICONTROL 目标] 仪表板 {#explore}

要导航到Platform UI中的目标仪表板，请选择 **[!UICONTROL 目标]** 然后，在左边栏中选择 **[!UICONTROL 概述]** 选项卡以显示仪表板。

最新快照的日期和时间显示在的顶部 [!UICONTROL 概述] ，位于目标下拉列表的旁边。 截至该日期和时间，所有构件数据都是准确的。 快照的时间戳以UTC格式提供；它不在单个用户或组织的时区内。

>[!NOTE]
>
>如果您的组织是初次使用Experience Platform，并且还没有有效的目标，则目标仪表板和 [!UICONTROL 概述] 选项卡不可见。 相反，选择 [!UICONTROL 目标] 左侧导航栏中显示 [!UICONTROL 目录] 选项卡。 要了解有关 [!UICONTROL 目录] 选项卡，请参阅 [[!UICONTROL 目标] workspace指南](../../destinations/ui/destinations-workspace.md).

![突出显示最新快照的Platform UI目标概述。](../images/destinations/snapshot-timestamp.png)

### 修改 [!UICONTROL 目标] 仪表板 {#modify}

选择 **[!UICONTROL 修改仪表板]** 以更改目标仪表板的外观。 这使您能够从仪表板移动、添加和删除构件，以及访问构件库。 从构件库中，您可以浏览可用的构件并为您的组织创建自定义构件。

请参阅 [修改仪表板](../customize/modify.md) 和 [构件库概述](../customize/widget-library.md) 文档，以了解更多信息。

### 添加构件 {#add-widget}

选择 **[!UICONTROL 添加构件]** 导航到构件库，然后查看要添加到仪表板的可用构件列表。

![突出显示添加构件的目标仪表板概述。](../images/destinations/destinations-overview-add-widget.png)

从构件库中，您可以浏览选择的标准和自定义受众构件。 有关如何添加构件的信息，请参阅构件库文档，了解如何 [添加构件](../customize/widget-library.md#add-widgets).

## 标准构件 {#standard-widgets}

Adobe提供了多个标准构件，可用于可视化与目的地相关的各种量度，并评估可用于数据分析的受众的完整性。 您还可以使用创建要与贵组织共享的自定义构件 [!UICONTROL 构件库]. 要了解有关创建自定义小部件的更多信息，请从阅读 [构件库概述](../customize/widget-library.md).

### 先决条件 {#prerequisites}

在继续描述标准构件之前，请确保您熟悉本文档中使用的以下关键术语的定义：

* **区段定义：** 区段定义是 **规则集** 用于描述目标受众的关键特征或行为。 这些规则包括属性和事件数据，可用于将用户档案视为受众的一部分。
* **受众：一组具有共同特征和行为的人员、帐户、家庭或其他实体。**
* **已映射/映射**：数据映射是将源数据字段映射到目标中相关目标字段的过程。
* **身份**：身份是唯一代表单个客户的标识符，例如Cookie ID、设备ID或电子邮件ID。
* **激活**：激活是用户为了将Oracle或配置文件映射到目标而采取的操作，例如Audience Eloqua、Google或SalesforceMarketing Cloud。

要详细了解每个可用的标准构件，请从以下列表中选择构件的名称：

* [[!UICONTROL 最常用目标]](#most-used-destinations)
* [[!UICONTROL 最近创建的目标]](#recently-created-destinations)
* [[!UICONTROL 最近激活的受众]](#recently-activated-audiences)
* [[!UICONTROL 按目标列出的最近激活的受众]](#recently-activated-audiences-by-destination)
* [[!UICONTROL 受众规模趋势]](#audience-size-trend)
* [[!UICONTROL 按身份显示的未映射受众]](#unmapped-audiences-by-identity)
* [[!UICONTROL 按身份映射的受众]](#mapped-audiences-by-identity)
* [[!UICONTROL 普通受众]](#common-audiences)
* [[!UICONTROL 映射的受众]](#mapped-audiences)
* [[!UICONTROL 映射的受众健康]](#mapped-audience-health)
* [[!UICONTROL 目标计数]](#destinations-count)
* [[!UICONTROL 目标状态]](#destination-status)
* [[!UICONTROL 按目标平台列出的活动目标]](#active-destinations-by-destination-platform)
* [[!UICONTROL 所有目标中的已激活受众]](#activated-audiences-across-all-destinations)
* [[!UICONTROL 激活的受众]](#activated-audiences)

### [!UICONTROL 最常用目标] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="最常用目标"
>abstract="此构件可按映射的受众数量显示贵组织最活跃的目标。 这些数字在上次拍摄快照时是准确的。此排名提供了对当前使用最多的目标的洞察，并突出显示了可能未被充分利用的目标。"

此 **[!UICONTROL 最常用的目标]** 构件按映射受众的数量显示您组织的顶级目标（截至最后一个快照）。 此排名可让您深入了解哪些目标正在被利用，同时还可能会显示那些可能未被充分利用的目标。

例如，如果您昨天配置了一个目标，但尚未将任何受众映射到该目标，则可以看到该目标当前未得到充分利用。

中显示的映射受众数量 [!UICONTROL 受众计数] 列自上次每日快照以来是准确的。 将新受众映射到目标时，只有在拍摄下一个快照后才会更新计数。

从小部件上显示的列表中选择目标的名称，以导航到该特定目标的目标详细信息。 您还可以选择 **[!UICONTROL 查看全部]** 导航到 **[!UICONTROL 浏览]** 选项卡，然后选择目标的名称以查看其详细信息。

![突出显示最常用目标小组件的目标仪表板的概述选项卡。](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近创建的目标] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="最近创建的目标"
>abstract="此构件显示您组织内最近配置的目标的列表。"

此 **[!UICONTROL 最近创建的目标]** 利用小组件，可查看贵组织最近配置的目标列表。

显示的创建日期与上一个每日快照比较准确。 换言之，如果创建一个新目标，则在拍摄下一个快照之前，它不会显示在列表中。

从小组件上显示的列表中选择目标的名称，将转到从链接到的目标详细信息 **[!UICONTROL 浏览]** 选项卡。 您还可以选择 **[!UICONTROL 查看全部]** 导航到 **[!UICONTROL 浏览]** 选项卡，然后选择目标的名称以查看其详细信息。

要详细了解如何配置特定类型的目标，请访问 [目标文档](../../destinations/home.md).

![突出显示最近创建的目标小组件的目标仪表板的概述选项卡。](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近激活的受众] {#recently-activated-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="最近激活的受众"
>abstract="此构件提供最近映射到目标的受众列表。 此列表提供系统中正在使用的受众和目标的快照，并有助于对任何错误的映射进行故障诊断。"

此 **[!UICONTROL 最近激活的受众]** 构件提供最近映射到目标的受众列表。 此列表提供系统中正在使用的受众和目标的快照，并有助于对任何错误的映射进行故障诊断。

此 [!UICONTROL 已更新] 显示的日期显示上次将受众激活到目标的时间，并且对于上次每日快照而言是正确的。 换言之，如果您将受众激活到目标，则更新的日期将在拍摄下一个快照之后才会更改。

从小组件上显示的列表中选择受众的名称会转到受众详细信息。 您还可以选择 **[!UICONTROL 查看全部]** 导航到 [!UICONTROL 受众] [!UICONTROL 浏览] 选项卡，然后选择受众的名称以查看其详细信息。

有关使用Experience Platform受众的更多信息，请参阅 [分段服务概述](../../segmentation/home.md).

![突出显示最近激活的受众小部件的目标仪表板的概述选项卡。](../images/destinations/recently-activated-audiences.png)

### [!UICONTROL 按目标列出的最近激活的受众] {#recently-activated-audiences-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="按目标列出的最近激活的受众"
>abstract="此构件根据在概述下拉列表中选择的目标，以降序显示最近激活的前5个受众。"

此 **[!UICONTROL 按目标列出的最近激活的受众]** 构件根据在概述下拉列表中选定的目标，以降序显示最近激活的前5个受众。 它类似于 [!UICONTROL 最近激活的受众] 构件，但显示的数据 **仅限** 应用于所选目标。

此构件包含两个量度：受众名称和上次将受众激活到目标的日期。 显示的数据自上次每日快照以来一直正确。

您可以从显示的列表中选择受众名称，以查看受众的详细信息。

![按目标构件列出的最近激活的受众。](../images/destinations/recently-activated-audiences-by-destination.png)

请参阅的先决条件部分 [所用术语的定义](#prerequisites) 在此描述中。

### [!UICONTROL 受众规模趋势] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="受众规模趋势"
>abstract="此构件说明了受众中包含的每天发送到目标帐户的用户档案数。 可使用第一个下拉菜单调整受众趋势的时段。第二个小组件下拉菜单选择要分析的受众。 从概述下拉列表中选择目标。"

此 **[!UICONTROL 受众规模趋势]** 构件描述一段时间内映射到目标帐户的受众的个人资料计数之间的关系。 该构件使用折线图来说明受众中包含的每天发送到目标帐户的用户档案数。

可以使用第一个下拉菜单调整过去30天、90天或12个月的受众趋势时段。

第二个下拉菜单列出了可以发送到在仪表板顶部选择的目标帐户的每个可用受众。

![受众规模趋势构件。](../images/destinations/audience-size-trend.png)

此 **[!UICONTROL 受众规模趋势]** 构件提供 [!UICONTROL 字幕] 按钮进行修改。 选择 **[!UICONTROL 字幕]** 以打开自动字幕对话框。 机器学习模型通过分析图表和受众数据自动生成描述关键趋势和重要事件的字幕。

![受众规模趋势小部件的自动字幕对话框。](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL 按身份显示的未映射受众] {#unmapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="按身份显示的未映射受众"
>abstract="此构件列出了前五项 **未映射** 按给定目标和身份的降序身份计数排名的受众。 构件下拉列表中列出的筛选条件 ID 因概述页面顶部选择的目标帐户而异。"

此 **[!UICONTROL 按身份显示的未映射受众]** 构件列出了前五项 **未映射** 按给定目标和身份的降序身份计数排名的受众。 它突出显示了对根据所选ID映射到所选目标帐户最有帮助的受众。

目标ID下拉列表会筛选您的可用受众。 下拉列表中列出的筛选器ID会根据在概述页面顶部选择的目标帐户而发生更改。

identities列计算受众中可映射到在构件ID下拉列表中选择ID的源ID的数量。

![按身份分类的未映射受众。](../images/destinations/unmapped-audiences-by-identity.png)

请参阅的先决条件部分 [所用术语的定义](#prerequisites) 在此描述中。

### [!UICONTROL 按身份映射的受众] {#mapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="按身份映射的受众"
>abstract="此构件提供前五个列表 **已映射** 受众。 此列表按照受众中包含的源ID数量从高到低排序。 从构件标题下方的下拉菜单中选择要计算的目标 ID。构件下拉列表中可用的目标 ID 取决于在概述仪表板顶部选择的目标。"

此构件提供前五个列表 **已映射** 受众。 此列表按照受众中包含的源ID数量从高到低排序。 从构件标题下方的下拉菜单中选择要计算的目标 ID。从小组件中的下拉列表中可用的目标ID将根据在概述功能板顶部选择的目标帐户过滤器而更改。

![按标识划分的映射受众构件。](../images/destinations/mapped-audiences-by-identity.png)

此 **[!UICONTROL 按身份映射的受众]** 构件突出显示了在所选目标内成功定位促销活动用户档案商机的可能性。 有效的定向营销活动并不依赖于发送到目标的用户档案数量，而是依赖于可能与目标ID匹配的源ID的数量，以提供有用且可操作的数据。

### 普通受众 {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="普通受众"
>abstract="此构件提供在页面顶部选择的目标帐户中激活的前五个受众的列表，以及在构件下拉列表中选定的目标受众的列表。 受众列表是根据最近激活受众的时间顺序排列的。 顶部会显示最近激活的受众。"

此 **[!UICONTROL 常见受众]** 小组件提供了在页面顶部选择的目标帐户中激活的前五个受众列表，以及在小组件下拉列表中选定的目标受众列表。 受众列表是根据最近激活受众的时间顺序排列的。 顶部会显示最近激活的受众。

此 [!UICONTROL 受众规模] 列提供每个所列受众的个人资料总数。

![通用受众构件。](../images/destinations/common-audiences.png)

### 映射的受众 {#mapped-audiences}

此 [!UICONTROL 映射的受众] 构件显示可激活到页面顶部所选目标的已映射受众总数。

选择 **[!UICONTROL 受众]** 导航到“受众”功能板 [!UICONTROL 浏览] 选项卡。 此工作区显示贵组织的所有区段定义的列表。

![映射的受众构件。](../images/destinations/mapped-audiences.png)

### 映射的受众健康 {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="映射的受众健康"
>abstract="此构件提供最多20个映射受众的列表，这些受众的总配置文件计数与映射到该目标的30天平均受众规模至少相差一个标准差系数。 它为受众规模与过去 30 天平均值的离散度提供了计算量度。受众规模按从高到低的顺序进行排序。"

该小组件提供最多20个映射受众的列表，截至上次每日快照时，这些受众的总配置文件计数与映射到该目标的30天平均受众规模至少相差一个标准差系数。

简言之，它提供了一个计算量度，用于衡量过去30天内受众规模与平均值的差值。 它会比较今天的受众规模是否超出了过去30天数据中看到的历史标准差。

系统中的所有受众规模都按照从高到低的受众规模排序，如 [!UICONTROL 最新大小] 列。

如果映射的受众配置文件计数与过去30天平均映射的配置文件大小相差一个标准偏差之外，则这表示系统中存在异常，应进行调查。

如果受众位于 [!UICONTROL 映射的受众运行状况] 构件偏差较大，您应该参考受众规模趋势图并找到异常受众。 该趋势可以让您深入了解受众的健康状况。

>[!NOTE]
>
>映射的受众运行状况构件的默认大小可能会妨碍表信息。 请修改小部件的大小，以提高映射的受众名称和列标题的清晰度。 有关以下内容的指导，请参阅修改功能板文档 [如何调整构件大小](../customize/modify.md).

![映射的受众运行状况构件。](../images/destinations/mapped-audience-health.png)

### [!UICONTROL 目标计数] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="目标计数"
>abstract="此构件提供了可在系统内激活和交付受众的可用端点总数。此数目包含活动目标数和非活动目标数。"

此 [!UICONTROL 目标计数] 构件提供可在系统中激活和交付受众的可用端点总数。 此数目包含活动目标数和非活动目标数。

在总计数下，选择 **[!UICONTROL 目标]** 导航到目标浏览选项卡。 此页面列出了您迄今为止已建立连接的所有目标。

![目标计数构件。](../images/destinations/destinations-count.png)

### [!UICONTROL 目标状态] {#destination-status}

此 [!UICONTROL 目标状态] 构件将启用的目标总数显示为单个量度，并使用圆环图来说明启用目标和禁用目标之间的比例差异。

当光标悬停在圆环图的相应部分上时，启用或禁用的目标的单个计数会显示在对话框中。

![目标状态构件。](../images/destinations/destination-status.png)

### [!UICONTROL 按目标平台列出的活动目标] {#active-destinations-by-destination-platform}

该构件提供一个两列表格，以显示活动目标平台的列表以及每个目标平台的活动目标总数。 目标平台的列表按从高到低的顺序排列。

![按目标平台构件分类的活动目标。](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL 所有目标中的已激活受众] {#activated-audiences-across-all-destinations}

此 [!UICONTROL 所有目标中的已激活受众] 构件在一个量度中提供跨所有目标激活的受众总数。 此数字对最近的快照是准确的。

![所有目标小组件中的已激活受众。](../images/destinations/activated-audiences-across-all-destinations.png)

选择 **[!UICONTROL 受众]** 导航到目标 [!UICONTROL 浏览] 选项卡。 本页列出了所有已启用的目标和各种相关量度。 请参阅文档以了解有关 [[!UICONTROL 浏览] 选项卡](../../destinations/ui/destinations-workspace.md#browse).

请参阅的先决条件部分 [所用术语的定义](#prerequisites) 在此描述中。

### [!UICONTROL 激活的受众] {#activated-audiences}

此构件为激活到目标的受众总数提供单个量度。

![激活的受众构件。](../images/destinations/activated-audiences.png)

选择 **[!UICONTROL 受众]** 导航到目标仪表板的详细信息页面。 此 [!UICONTROL 激活数据] 选项卡显示已映射到目标的受众列表，包括其开始日期和结束日期（如果适用），以及用于数据导出的其他相关信息，如导出类型、时间表和频率。 要查看特定受众的详细信息，请从中选择其名称。 [!UICONTROL 受众名称] 列。

![突出显示了“激活数据”选项卡的目标仪表板详细信息页面。](../images/destinations/activation-data-tab.png)

此构件可帮助您根据一目了然激活的受众数量了解目标的价值。 通过它，还可以轻松地访问更详细的信息，以便进一步分析。

请参阅的先决条件部分 [所用术语的定义](#prerequisites) 在此描述中。

## 后续步骤

现在，通过阅读本文档，您应该能够找到目标仪表板，并了解可用构件中显示的量度。 要了解有关在Experience Platform中使用目标的更多信息，请参阅 [目标文档](../../destinations/home.md).
