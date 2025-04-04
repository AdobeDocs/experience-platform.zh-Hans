---
title: 同意分析和跟踪
description: 了解如何构建同意分析仪表板，以跟踪用户同意随时间变化的趋势。
exl-id: 34accae5-8b4f-4281-8333-187a91db8199
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# 同意分析和跟踪

在当今的营销形势下，您需要理解并尊重客户同意首选项。 Adobe Real-Time Customer Data Platform为营销人员提供了分析客户同意以建立信任、遵守隐私法规并提供更个性化体验的功能。

本文档详细介绍如何为Real-Time CDP数据的各种营销用例构建同意仪表板。 具体来说，它重点介绍如何根据您的业务需求创建具有适当属性的受众，然后通过在Adobe Experience Platform UI中使用预配置的构件来获取见解。 此外，还提供了使用用户定义的仪表板功能构建您自己的自定义小部件的另一种方法。

## 用例 {#use-cases}

本指南涵盖的使用案例是同意趋势和同意重叠。

- **同意趋势**&#x200B;跟踪用户同意随时间变化的趋势。 分析同意偏好设置更改可帮助营销人员规划和执行适应这些用户偏好设置更改的营销活动。 例如，您可能需要开展有针对性的教育活动、透明度和信任活动或激励活动以推动同意选择。 您还可以关联可能已对同意产生负面影响的营销活动，以主动降低这些营销活动的频率。
- **同意重叠**&#x200B;使用同意渠道之间的重叠，为同意多个渠道的客户在多个渠道上提供一致的个性化消息。 营销人员可以优先分配资源给某些渠道，在这些渠道中，更高程度的同意和个性化的消息传递可能会引起客户的共鸣，并产生更高的响应率。

## 创建同意的受众 {#create-consent-audiences}

要构建同意仪表板，您必须首先创建同意联系的所有用户档案的受众。 要导航到Real-Time Customer Data Platform区段生成器，请在Experience Platform UI的左侧导航中选择&#x200B;**[!UICONTROL 受众]**。 从[!UICONTROL 受众]仪表板的[!UICONTROL 客户]选项卡中，选择视图右上角的&#x200B;**[!UICONTROL 创建受众]**，然后选择&#x200B;**[!UICONTROL 生成规则]**。

突出显示具有[!UICONTROL 客户]、[!UICONTROL 受众]和[!UICONTROL 创建区段]的[!UICONTROL 受众]仪表板。](../images/insights-use-cases/consent-analysis/create-audience.png)![

此时将显示“区段生成器”。 接下来，从可用选项中选择&#x200B;**[!UICONTROL XDM Individual Profile]**。 有关[规则生成器画布](../../segmentation/ui/segment-builder.md#rule-builder-canvas)的详细信息，请参阅文档。

![突出显示具有[!UICONTROL XDM个人配置文件]属性文件夹的区段生成器。](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

从可用的选项中找到您的同意属性。 选择&#x200B;**[!UICONTROL 同意和偏好设置]**。

>[!NOTE]
>
>如果您在与Adobe推荐字段组不同的属性中维护了用户同意，则必须选择这些属性，而不是下面显示的属性。

有关分段](../../segmentation/tutorials/consents.md#handling-consent-in-segmentation)文档中[同意处理的更多信息。

![带有[!UICONTROL 同意和首选项]属性文件夹的区段生成器突出显示。](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

将显示各种同意和偏好设置选项。 由于此演示侧重于同意通过各种营销渠道进行联系，因此请选择&#x200B;**[!UICONTROL 营销偏好设置]**。

![突出显示具有[!UICONTROL 营销首选项]文件夹的区段生成器。](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

将显示营销偏好设置列表。 虽然此示例用例侧重于电子邮件、短信和调用，但您也可以为任何其他组合或整个选项构建见解。 对于每个渠道，执行以下步骤以创建受众。

要开始配置受众，请选择&#x200B;**[!UICONTROL 接收短信]** / **[!UICONTROL 接收电子邮件]** / **[!UICONTROL 接收呼叫]**。

![受众生成器中突出显示营销的可用联系渠道。](../images/insights-use-cases/consent-analysis/channels.png)

将显示[!UICONTROL 订阅]文件夹。 从可用选项中，选择&#x200B;**[!UICONTROL 选择值]**&#x200B;属性并将其拖动到中心窗格，然后从下拉列表中选择所需的值。 在这种情况下，请选择&#x200B;**是（选择启用）**。 接下来，根据业务需求为受众命名，并提供用户友好的描述。

>[!NOTE]
>
>建议您创建的受众数量存在软限制。 有关详细信息，请参阅[分段护栏文档](../../profile/guardrails.md#segmentation-guardrails)。

![区段生成器中突出显示[!UICONTROL 是（选择加入）]值的[!UICONTROL 选择值]属性。 受众的名称和描述也突出显示。](../images/insights-use-cases/consent-analysis/choice-value.png)

创建必要的受众后，这些受众将列在[!UICONTROL 受众] [!UICONTROL 浏览]选项卡中。

>[!NOTE]
>
>创建受众时，您必须等待批量分段作业完成，然后才有数据可用来开始构建同意仪表板。 批量分段描述了通过区段定义一次移动所有用户档案数据以产生相应受众的过程。 创建受众后，将保存并存储该受众以供您导出和使用。 每24小时自动评估批处理客户细分。

## 使用洞察 {#consume-insights}

Adobe已创建各种见解，这些见解自动在“用户档案”、“受众”和“目标”功能板中为您提供。 然后，您创建的任何受众都将自动可用于这些预配置的见解。 有关[配置文件](../guides/profiles.md#standard-widgets)、[受众](../guides/audiences.md#standard-widgets)和[目标](../guides/destinations.md)功能板中可用的分析列表，请参阅标准构件文档。

## 受众重叠 {#audience-overlap}

要检查任意两个同意受众之间的重叠，请将[!UICONTROL 按合并策略列出的受众重叠]添加到您的配置文件仪表板，然后在下拉菜单中选择所需的受众。 有关洞察的更多信息，请参阅文档，了解如何将&#x200B;[*按合并策略*](../guides/profiles.md#audience-overlap-by-merge-policy)&#x200B;划分的受众重叠添加到功能板。

<!-- Image needs updating to night mode -->

![突出显示具有按合并策略小组件划分的受众重叠的用户档案仪表板。 该小组件显示两个同意受众之间的重叠。](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

您可以使用受众仪表板中的受众重叠报表查看所有受众的重叠，其中用户已同意接收所有其他受众的呼叫。 要查看同意受众的重叠，请先导航到[!UICONTROL 受众] [!UICONTROL 概述]选项卡。 从该位置，您可以将[!UICONTROL 受众重叠报表]构件添加到受众仪表板。 创建构件后，从页面顶部的受众概述下拉菜单中选择&#x200B;**[!UICONTROL 用户同意调用]**&#x200B;受众。 接下来，在受众重叠报表小组件中选择&#x200B;**[!UICONTROL 查看更多]**，以查看最多50个顶部重叠，以及有关所选区段的最少重叠中的50个。

<!-- Image needs updating to night mode -->

![显示具有受众重叠报表小组件的受众仪表板。 用户同意调用受众作为比较受众，并且查看更多链接都突出显示。](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

将展开受众重叠报表对话框，以显示其他受众重叠数据。

<!-- Image needs updating to night mode -->

![受众重叠报表，其中突出显示了用户同意发送电子邮件的受众。](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## 受众规模趋势 {#audience-size-trends}

创建基于同意的受众时，会自动显示自创建受众日期起最多12个月的趋势。 要获得客户同意的完整功能趋势，请将以下构件添加到[!UICONTROL 区段] [!UICONTROL 概述]页面。 这些见解提供了一种强大的手段，用于跟踪您的同意如何随时间变化。 它们甚至与您并行运行的任何可能对同意产生正面或负面影响的活动相关联。 为这些构件提供的描述适用于同意用例。

- [受众规模趋势](../guides/audiences.md#audience-size-trend)：此构件提供了一种跟踪您的同意如何随时间的变化的方法。
- [受众规模变化趋势](../guides/audiences.md#audience-size-change-trend)：此构件跟踪您的客户同意如何每天发生更改。 例如，如果客户同意的数量减少了100,000，则可以查看每天发生的更改。
- [按身份划分的受众规模趋势](../guides/audiences.md#audience-size-trend-by-identity)：利用此小组件，您可以跟踪各自同意意见随时间的变化，但按特定身份（如电子邮件）进一步过滤。

<!-- Image needs updating to night mode -->

![显示受众规模趋势、按身份划分的受众规模趋势和受众规模变化趋势小组件的受众仪表板。 已突出显示同意接收电子邮件受众的用户。](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## 受众概述功能板 {#audiences-overview-dashboard}

创建同意相关的受众（例如“用户同意短信”）后，您可以通过向受众概述仪表板添加相应的小部件，查看有关受众的关键个性化同意信息。 导航到[!UICONTROL 受众] [!UICONTROL 概述]，并从构件库中添加您选择的构件。 添加到仪表板视图的任何构件都可以使用[!UICONTROL 修改仪表板]功能调整大小和移动。 您的个性化视图可以包含各种见解，例如一段时间的趋势（最多12个月）、与其他受众的重叠以及受众的身份构成。 下面显示了一个示例视图。

![用户同意短信受众的受众仪表板在全局受众下拉菜单中突出显示。](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## 用户定义的仪表板 {#usr-defined-dashboards}

您还可以使用用户定义的仪表板构建自己的小组件。 通过构建您自己的构件，您可以完全控制构件的类型，还可以灵活地直接在Adobe Real-Time CDP中添加过滤器等。

例如，如果您希望在同一图表中显示多个同意受众的趋势，以便了解每个同意偏好设置随时间的变化。 通过用户定义的功能板，只需最少的步骤和一次性设置即可实现此类型的可视化。 首先，在左侧导航中选择&#x200B;**[!UICONTROL 功能板]**。 将显示[!UICONTROL 功能板]工作区。 然后选择&#x200B;**[!UICONTROL 创建仪表板]**。 有关如何[创建功能板和自定义小组件](../standard-dashboards.md)的完整说明，请参阅用户定义的功能板指南。

![突出显示包含功能板和创建功能板的功能板工作区。](../images/standard-dashboards/create-dashboard.png)

当在小组件编辑器中[选择数据模型](../standard-dashboards.md#select-data-model)时，依次选择`CDPInsights`和&#x200B;**[!UICONTROL 下一步]**。 出现[!UICONTROL 选择表]对话框。

![突出显示了CDPInsights模型的“选择数据模型”对话框。](../images/standard-dashboards/select-data-model-dialog.png)

下一个视图在左边栏中显示可用表的列表。 选择 `adwh_fact_profile_by_segment_and_namespace_trendlines`。

![突出显示了“adwh_fact_profile_by_segment_and_namespace_trendlines”表的“选择表”对话框。](../images/insights-use-cases/consent-analysis/select-table.png)

使用所选表中的数据填充构件编辑器后，请执行以下步骤：

- [搜索[!UICONTROL 属性]](../standard-dashboards.md#add-filter-attributes)以查找`[!UICONTROL date]`，然后使用+图标从下拉菜单中将`[!UICONTROL date]`属性添加到X轴。
  ![突出显示添加图标和下拉菜单的小组件编辑器。](../images/standard-dashboards/attributes-dropdown.png)
- 在[!UICONTROL 属性]中搜索`[!UICONTROL count_of_profiles]`，然后使用+图标将`[!UICONTROL count_of_profiles]`属性从下拉菜单添加到Y轴。
- 选择[!UICONTROL Y轴]字段中的`...`（省略号）图标，然后从下拉菜单中选择[!UICONTROL SUM]聚合函数。
  ![小组件编辑器同意显示小组件趋势，其中数据模型、表格和Y轴下拉菜单及SUM功能突出显示。](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- 选择[!UICONTROL 标记]下拉菜单，并将图表类型更改为[!UICONTROL 线]。
- 在[!UICONTROL 属性]中搜索`[!UICONTROL segment_name]`，然后使用+图标将`segment_name`添加为下拉菜单中的[!UICONTROL 筛选器]。 将显示[!UICONTROL 筛选器：区段名称]对话框。 选择之前创建的与同意相关的受众。 对于此示例，请选择&#x200B;**[!UICONTROL 用户同意呼叫]**、**[!UICONTROL 用户同意短信]**&#x200B;和&#x200B;**[!UICONTROL 用户同意电子邮件]**，然后依次选择&#x200B;**[!UICONTROL 应用]**。
- 在[!UICONTROL 属性]中搜索`[!UICONTROL segment_name]`，然后从下拉菜单中选择+图标以将`segment_name`添加为[!UICONTROL 颜色]。
- 打开[[!UICONTROL 属性]面板](../standard-dashboards.md#widget-properties)并提供适当的[!UICONTROL 小组件标题]和[!UICONTROL 轴标签]。
  ![突出显示属性图标和小组件标题的小组件编辑器。](../images/standard-dashboards/properties-panel.png)
- 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以确认您的设置。

>[!TIP]
>
>在保存仪表板之前，您现在可以调整小部件的大小或将其移动到所需的大小和位置。


下图演示了已完成的构件的显示方式以及其他潜在的自定义分析。 有关可创建的构件类型的更多详细信息，请参阅[数据模型文档](../data-models/cdp-insights-data-model-b2c.md)。

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![完成的自定义同意趋势小组件。](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## 跟踪同意政策 {#consent-policies}

您创建的同意仪表板仅捕获同意和偏好设置属性的&#x200B;**分布**。

>[!NOTE]
>
>对于&#x200B;**Adobe Healthcare Shield**&#x200B;或&#x200B;**Adobe Privacy &amp; Security Shield**&#x200B;的客户，这些功能板&#x200B;**不**&#x200B;反映对同意政策的任何跟踪。 可用跟踪包括已创建、已启用的策略的数量，以及对受众成员资格的影响。

## 后续步骤

通过阅读本文档，您已了解如何使用Real-Time CDP Insights构建功能板，以全面查看客户同意首选项。 本文档演示了Real-Time CDP如何为当今以隐私为中心的环境提供可靠的解决方案，在这些环境中，基于同意数据的收集、分段、分析和个性化营销活动对营销人员至关重要。
