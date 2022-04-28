---
keywords: Experience Platform；主页；热门主题；监视帐户；监视数据流；数据流；目标
description: 利用目标，可从Adobe Experience Platform向无数外部合作伙伴激活数据。 本教程提供了有关如何使用Experience Platform用户界面监控目标数据流的说明。
solution: Experience Platform
title: 在UI中监控目标的数据流
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 2be8ed7daaac6554bdbc52acab325a474fa87566
workflow-type: tm+mt
source-wordcount: '3200'
ht-degree: 0%

---

# 在UI中监控目标的数据流

利用目标，可从Adobe Experience Platform向无数外部合作伙伴激活数据。 Platform通过提供数据流的透明度，使跟踪数据到目标的流程变得更加轻松。

监控仪表板可直观地表示数据流的历程，包括数据被激活到的目标。 本教程提供了有关如何直接在目标工作区中监控数据流或使用监控功能板通过Experience Platform用户界面监控目标的数据流的说明。

## 快速入门 {#getting-started}

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [数据流](../home.md):数据流是跨平台移动数据的数据作业的表示形式。 数据流是跨不同的服务进行配置的，有助于将数据从源连接器移动到目标数据集，并 [!DNL Identity] 和 [!DNL Profile]和 [!DNL Destinations].
   - [数据流运行](../../sources/notifications.md):数据流运行是基于所选数据流的频率配置的定期计划作业。
- [目标](../../destinations/home.md):目标是与常用应用程序的预建集成，允许从平台无缝激活数据以用于跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

## 在目标工作区中监控数据流 {#monitor-dataflows-in-the-destinations-workspace}

在 **[!UICONTROL 目标]** 工作区中，导航到 **[!UICONTROL 浏览]** 选项卡，然后选择要查看的目标名称。

![选择目标视图](../assets/ui/monitor-destinations/select-destination.png)

将显示现有数据流的列表。 本页列出了可查看的数据流，包括有关其目标、用户名、数据流数量和状态的信息。

有关状态的更多信息，请参阅下表：

| 状态 | 描述 |
| ------ | ----------- |
| 已启用 | 的 `Enabled` 状态表示数据流处于活动状态，并正在根据提供的计划导出数据。 |
| 已禁用 | 的 `Disabled` 状态表示数据流处于非活动状态，且未导出任何数据。 |
| 处理时间 | 的 `Processing` 状态表示数据流尚未处于活动状态。 此状态通常会在创建新数据流后立即出现。 |
| 错误 | 的 `Error` 状态表示数据流的激活过程已中断。 |

### 为流目标运行数据流 {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="数据流运行详细信息"
>abstract="目标数据流运行详细信息包含有关区段激活状态的信息以及从实时客户配置文件获取的用于生成唯一标识的量度。 要了解更多信息，请查阅量度定义指南。"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="收到的用户档案"
>abstract="数据流中接收的用户档案总数。 此值每60分钟更新一次。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="已激活身份"
>abstract="成功激活到选定目标的单个配置文件标识的计数。 此量度包含从导出区段中创建、更新和删除的标识。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="排除的身份"
>abstract="根据缺少属性和同意违规，从选定目标的激活中排除的单个配置文件记录计数。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="身份失败"
>abstract="所选目标的单个配置文件标识的计数失败。 有关详细信息，请检查错误诊断。"

对于流目标， [!UICONTROL 数据流运行] 选项卡会每小时更新数据流运行中的量度数据。 标有的最显着的统计数据是关于身份的。

标识表示用户档案的不同方面。 例如，如果某个用户档案同时包含电话号码和电子邮件地址，则该用户档案将具有两个身份。

将显示单个运行及其特定量度的列表，以及以下身份总数：

- **[!UICONTROL 已激活身份]**:成功激活到选定目标的用户档案标识总数。 此量度包含从导出区段中创建、更新和删除的标识。
- **[!UICONTROL 排除的身份]**:根据缺少属性和同意违规跳过以进行激活的配置文件标识的总数。
- **[!UICONTROL 身份失败]**:由于错误而未激活到目标的配置文件标识的总数。

![数据流运行流目标的详细信息](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

每个数据流运行都显示以下详细信息：

- **[!UICONTROL 数据流运行开始]**:数据流运行开始的时间。 对于流数据流运行，Experience Platform会根据数据流运行的开始以每小时量度的形式捕获量度。 对于流数据流运行，如果数据流运行（例如在晚上10:30启动），则量度会在UI中将开始时间显示为晚上10:00。
- **[!UICONTROL 处理时间]**:数据流运行处理所花费的时间。
   - 对于 **[!UICONTROL 已完成]** 运行时，处理时间量度始终显示1小时。
   - 对于仍在 **[!UICONTROL 处理]** 状态下，用于捕获所有量度的窗口将保持打开状态超过一小时，用于处理与数据流运行对应的所有量度。 例如，从上午9:30开始的数据流运行可能会保持处理状态1小时30分钟，以捕获和处理所有量度。 然后，一旦处理窗口关闭，并且数据流运行的状态将更新为 **已完成**，则显示的处理时间会更改为1小时。
- **[!UICONTROL 收到的用户档案]**:数据流中接收的用户档案总数。
- **[!UICONTROL 已激活身份]**:在数据流运行中成功激活到选定目标的配置文件标识总数。 此量度包含从导出区段中创建、更新和删除的标识。
- **[!UICONTROL 排除的身份]**:根据缺少属性和同意违规从激活中排除的配置文件标识总数。
- **[!UICONTROL 身份失败]** 由于错误而未激活到目标的配置文件标识的总数。
- **[!UICONTROL 激活率]**:已成功激活或跳过的已接收身份的百分比。 以下公式演示了如何计算此值：
   ![激活率公式](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL 状态]**:表示数据流处于的状态：e [!UICONTROL 已完成] 或 [!UICONTROL 处理]. [!UICONTROL 已完成] 表示在1小时内导出了相应数据流运行的所有标识。 [!UICONTROL 处理] 表示数据流运行尚未完成。

要查看特定数据流运行的详细信息，请从列表中选择运行的开始时间。

数据流运行的详细信息页面包含其他信息，如接收的用户档案数、激活的标识数、失败的标识数和排除的标识数。

![流目标的数据流详细信息](../assets/ui/monitor-destinations/dataflow-details-stream.png)

详细信息页面还显示失败的身份和排除的身份的列表。 将显示失败和排除的身份的信息，包括错误代码、身份计数和描述。 默认情况下，列表会显示失败的标识。 要显示跳过的标识，请选择 **[!UICONTROL 排除的身份]** 切换。

![流目标的数据流记录](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### 为批处理目标运行数据流 {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="数据流运行详细信息"
>abstract="目标数据流运行详细信息包含有关区段激活状态的信息以及从实时客户配置文件获取的用于生成唯一标识的量度。 要了解更多信息，请查阅量度定义指南。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html#dataflow-runs-for-streaming-destinations" text="为流目标运行数据流"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="收到的用户档案"
>abstract="数据流中接收的用户档案总数。 此值每60分钟更新一次。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="已激活身份"
>abstract="成功激活到选定目标的单个配置文件标识的计数。 此量度包含从导出区段中创建、更新和删除的标识。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="排除的身份"
>abstract="根据缺少属性和同意违规，从选定目标的激活中排除的单个配置文件记录计数。"

对于批处理目标， [!UICONTROL 数据流运行] 选项卡提供有关数据流运行的量度数据。 将显示单个运行及其特定量度的列表，以及以下身份总数：

- **[!UICONTROL 已激活身份]**:成功激活到选定目标的用户档案标识总数。 此量度包含从导出区段中创建、更新和删除的标识。
- **[!UICONTROL 排除的身份]**:根据缺少属性和同意违规，从选定目标的激活中排除的单个配置文件标识计数。

![数据流运行批处理目标的视图](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

每个数据流运行都显示以下详细信息：

- **[!UICONTROL 数据流运行开始]**:数据流运行开始的时间。
- **[!UICONTROL 处理时间]**:处理数据流运行所花费的时间。
- **[!UICONTROL 收到的用户档案]**:数据流中接收的用户档案总数。 此值每60分钟更新一次。
- **[!UICONTROL 已激活身份]**:在数据流运行中成功激活到选定目标的配置文件标识总数。 此量度包含从导出区段中创建、更新和删除的标识。
- **[!UICONTROL 排除的身份]**:根据缺少属性和同意违规从激活中排除的配置文件标识总数。
- **[!UICONTROL 状态]**:表示数据流处于的状态。 这可以是三种状态之一： [!UICONTROL 成功], [!UICONTROL 失败]和 [!UICONTROL 处理]. [!UICONTROL 成功] 表示数据流处于活动状态，并正在根据其提供的时间表导出数据。 [!UICONTROL 失败] 表示由于错误，数据激活已挂起。 [!UICONTROL 处理] 表示数据流尚未处于活动状态，通常在创建新数据流时会遇到该数据流。

要查看特定数据流运行的详细信息，请从列表中选择运行的开始时间。

>[!NOTE]
>
>根据目标数据流的调度频率生成数据流运行。 将针对每个数据流分别运行一个单独的数据流 [合并策略](../../profile/merge-policies/overview.md) 应用于区段。

数据流的详细信息页面除了数据流列表中显示的详细信息之外，还显示有关数据流的更多具体信息：

- **[!UICONTROL 数据大小]**:要导出的数据流的大小。
- **[!UICONTROL 文件总数]**:数据流中导出的文件总数。
- **[!UICONTROL 上次更新时间]**:上次更新数据流运行的时间。

![批处理目标的数据流运行详细信息](../assets/ui/monitor-destinations/dataflow-batch.png)

详细信息页面还显示失败的身份和排除的身份的列表。 将显示失败和排除的标识的信息，包括错误代码和描述。 默认情况下，列表会显示失败的标识。 要显示排除的身份，请选择 **[!UICONTROL 排除的身份]** 切换。

![批处理目标的数据流记录](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## 监控目标功能板 {#monitoring-destinations-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="激活"
>abstract="目标激活视图包含有关区段激活状态的信息以及从实时客户配置文件获取的用于生成唯一标识的量度。"

访问 [!UICONTROL 监控] 功能板，选择 **[!UICONTROL 监控]** (![监控图标](../assets/ui/monitor-destinations/monitoring-icon.png))。 在 [!UICONTROL 监控] 页面，选择 [!UICONTROL 目标]. 的 [!UICONTROL 监控] 功能板包含有关目标运行作业的量度和信息。

>[!NOTE]
>
>- 目前，Experience Platform中所有目标都支持目标监控功能 *除外* the [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化](/help/destinations/catalog/personalization/custom-personalization.md) 目标。
>- 对于 [AmazonKinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md) 目标、排除的标识当前不会显示。


使用 [!UICONTROL 目标] 功能板，全面了解激活流的运行状况。 首先，深入了解所有批处理和流目标的汇总级别，然后深入了解数据流、数据流运行和激活区段的详细视图，以便深入查看激活数据。 屏幕 [!UICONTROL 监控] 功能板通过量度和错误描述提供可操作的洞察，以帮助您解决激活方案中可能出现的任何问题。

功能板的中心是 [!UICONTROL 激活] 面板，其中包含量度和图表，用于显示导出到流目标的数据的激活率以及运行到批处理目标的失败批处理数据流的数据。

![流式和批量激活图](../assets/ui/monitor-destinations/dashboard-graph.png)


默认情况下，显示的数据包含过去24小时内的激活信息。 选择 **[!UICONTROL 最近24小时]** 来调整显示记录的时间范围。 可用选项包括 **[!UICONTROL 最近24小时]**, **[!UICONTROL 最近7天]**&#x200B;和 **[!UICONTROL 最近30天]**. 或者，您也可以在显示的日历弹出窗口中选择日期。 选择日期后，选择 **[!UICONTROL 应用]** 来调整所显示信息的时间范围。

>[!NOTE]
>
>以下屏幕截图显示了过去30天（而不是过去24小时）内的激活率和批量数据流运行情况。 您可以通过选择 **[!UICONTROL 最近30天]**.

![更改激活目标的回顾日期范围](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

使用箭头图标(![箭头图标](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png))以展开或关闭屏幕顶部的卡片，这些卡片会根据目标类型（流播放或批量播放）显示有关激活详细信息的概览：

- **[!UICONTROL 流激活率]**:表示已成功激活或跳过的已接收身份的百分比。 用于计算此百分比的公式在本页的 [为流目标运行数据流](#dataflow-runs-for-streaming-destinations) 中。
- **[!UICONTROL 批处理失败的数据流运行]**:表示在选定时间间隔内运行的失败数据流数。

![在页面顶部显示或关闭信息卡](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

的 **[!UICONTROL 激活]** 默认情况下会显示图表，您可以禁用该图表以展开下面的目标列表。 选择 **[!UICONTROL 量度和图表]** 切换以禁用图形。

的 **[!UICONTROL 激活]** 面板会显示至少包含一个现有帐户的目标列表。 此列表还包含有关以下目标的用户档案信息：已接收的用户档案、已激活的身份、身份失败、已排除的身份、激活率、失败的数据流总数以及上次更新日期。 并非所有量度都适用于所有目标类型。 下表概述了按目标类型、流量或批量提供的量度。

| 量度 | 目标类型 |
---------|----------|
| **[!UICONTROL 收到的用户档案]** | 流式处理和批处理 |
| **[!UICONTROL 已激活身份]** | 流式处理和批处理 |
| **[!UICONTROL 身份失败]** | 流 |
| **[!UICONTROL 排除的身份]** | 流式处理和批处理 |
| **[!UICONTROL 激活率]** | 流 |
| **[!UICONTROL 失败的数据流总数]** | 批次 |
| **[!UICONTROL 上次更新时间]** | 流式处理和批处理 |

![功能板中所有激活的目标](../assets/ui/monitor-destinations/dashboard-destinations.png)

您还可以过滤目标列表，以仅显示选定的目标类别。 选择 **[!UICONTROL 我的目标]** 下拉列表，然后选择 [目标类别](/help/destinations/destination-types.md#categories) 过滤到的。

![使用下拉选择器筛选目标](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

此外，您还可以在搜索栏中输入目标，以隔离到单个目标。 如果要查看目标的数据流，可以选择过滤器 ![过滤器](../assets/ui/monitor-destinations/filter-add.png) 查看其活动数据流的列表。

![使用搜索栏过滤目标](../assets/ui/monitor-destinations/filtered-destinations.png)

如果要查看所有目标中的所有现有数据流，请选择 **[!UICONTROL 数据流]**.

此时会出现一个数据流列表，它按上次数据流运行进行排序。 通过查找要监视的目标并选择过滤器，可以查看特定数据流的其他详细信息 ![过滤器](../assets/ui/monitor-destinations/filter-add.png) 旁边，然后选择过滤器 ![过滤器](../assets/ui/monitor-destinations/filter-add.png) 数据流旁边。

![监控仪表板中突出显示的所有数据流](../assets/ui/monitor-destinations/dashboard-dataflows.png)

选择数据流以供进一步检查后，“数据流详细信息”页包含一个切换开关，通过该切换开关，您可以查看数据流中的已激活数据（按数据流运行或区段划分）。

### 数据流运行视图 {#dataflow-runs-view}

When **[!UICONTROL 数据流运行]** 选中后，您可以看到所选数据流的数据流运行列表以及有关每个运行的更多信息。

>[!INFO]
>
>对于流目标的数据流，数据流运行会按小时划分。 每个每小时窗口都会生成一个对应的数据流运行ID。
>
>对于到批处理目标的数据流，每个区段都会根据区段激活计划频率生成相应的数据流运行。 例如，如果为同一目标数据流中的五个区段设置每日计划激活，则每天将生成五个单独的数据流运行。

![“流”运行面板](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

使用 **[!UICONTROL 仅显示失败]** 切换以仅显示数据流的失败运行。

![数据流运行 — 仅显示失败切换](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### 区段级别视图 {#segment-level-view}

When **[!UICONTROL 区段]** ，则您会看到选定时间范围内已激活选定数据流的区段列表。 此屏幕包含有关已激活身份、已排除身份以及上次数据流运行的状态和时间的区段级别信息。 通过查看排除和激活的标识的量度，您可以验证区段是否成功激活。

例如，您要将名为“加州忠诚会员”的区段激活到Amazon S3目标“加州忠诚会员12月”。 假设选定区段中有100个用户档案，但100个用户档案中只有80个包含忠诚度ID属性，并且您已将导出映射规则定义为 `loyalty.id` 必需。 在这种情况下，在区段级别，您将看到激活了80个身份，并排除20个身份。

>[!IMPORTANT]
>
>请注意与区段级别量度相关的当前限制：
>- 区段级别视图当前仅适用于批处理目标。
>- 当前仅为成功的数据流运行记录区段级别量度。 对于失败的数据流运行和排除的记录，不会记录它们。


![数据流面板中的区段](../assets/ui/monitor-destinations/dashboard-segments-view.png)

在区段级别视图中，这些量度是在选定时间范围内跨多个数据流运行进行聚合。 如果有多个数据流运行，您可以从区段级别向下展开以查看按选定区段过滤的每个数据流运行的划分。
使用过滤器按钮 ![过滤器](../assets/ui/monitor-destinations/filter-add.png) 要深入到数据流中每个区段的数据流运行视图，请执行以下操作：

### “数据流运行”页 {#dataflow-runs-page}

“数据流运行”页显示有关数据流运行的信息，包括数据流运行开始时间、处理时间、收到的用户档案、激活的身份、排除的身份、身份失败、激活速率和状态。

当您从 [区段级别视图](#segment-level-view)，则可以选择通过以下选项过滤运行的数据流：

- **[!UICONTROL 数据流以失败身份运行]**:对于选定的区段，此选项列出所有因激活而失败的数据流运行。 要检查特定数据流运行中的身份失败的原因，请参阅 [“数据流运行详细信息”页](#dataflow-run-details-page) 对于数据流运行。
- **[!UICONTROL 数据流以跳过的标识运行]**:对于选定的区段，此选项会列出在某些身份未完全激活且跳过某些配置文件的情况下运行的所有数据流。 要检查为何会跳过特定数据流运行中的标识，请参阅 [“数据流运行详细信息”页](#dataflow-run-details-page) 对于数据流运行。
- **[!UICONTROL 数据流使用激活的身份运行]**:对于选定的区段，此选项会列出已成功激活身份的所有数据流运行。

![过滤区段的数据流运行](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

要查看有关特定数据流运行的更多详细信息，请选择过滤器 ![过滤器](../assets/ui/monitor-destinations/filter-add.png) 在“数据流运行开始时间”旁边，查看“数据流运行详细信息”页。

![数据流在监控仪表板中运行过滤器](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### “数据流运行详细信息”页 {#dataflow-run-details-page}

数据流运行详细信息页面除了数据流运行列表中显示的详细信息之外，还显示有关数据流的更多具体信息：

- **[!UICONTROL 数据流运行ID]**:数据流的ID。
- **[!UICONTROL IMS组织ID]**:数据流所属的IMS组织。
- **[!UICONTROL 上次更新时间]**:上次更新数据流运行的时间。

详细信息页面还具有一个切换开关，用于在数据流运行错误和区段之间切换。 此选项仅适用于在批处理目标中运行的数据流。

数据流运行错误视图显示失败身份和已排除身份的列表。 将显示失败和排除的身份的信息，包括错误代码、身份计数和描述。 默认情况下，列表会显示失败的标识。 要显示跳过的标识，请选择 **[!UICONTROL 排除的身份]** 切换。

![排除的身份切换](../assets/ui/monitor-destinations/identities-excluded.png)

When **[!UICONTROL 区段]** 选中后，您将看到在所选数据流运行中激活的区段列表。 此屏幕包含有关已激活身份、已排除身份以及上次数据流运行的状态和时间的区段级别信息。

![数据流运行 — 区段视图](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## 后续步骤 {#next-steps}

通过阅读本指南，您现在知道如何监控批处理和流目标的数据流，包括所有相关信息，如处理时间、激活率和状态。 要进一步了解Platform中的数据流，请阅读 [数据流概述](../home.md). 要了解有关目标的更多信息，请阅读 [目标概述](../../destinations/home.md).