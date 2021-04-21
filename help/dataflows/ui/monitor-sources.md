---
keywords: Experience Platform；主页；热门主题；监视帐户；监视数据流；数据流；源
description: 本教程提供了使用聚合监视视图和跨服务监视来监视数据流的步骤。
solution: Experience Platform
title: 监视UI中源的数据流
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 0%

---

# 监视UI中源的数据流

在Adobe Experience Platform，数据是从各种来源中摄取的，在Experience Platform中分析，并激活到各种目的地。 平台通过为数据流提供透明度，使跟踪这种可能的非线性数据流的过程更加容易。

监视仪表板可直观地呈现数据流的旅程。 您可以使用聚合监控视图，并从源级别垂直导航到数据流，以及数据流运行，从而使您能够视图对数据流成功或失败做出贡献的相应量度。 您还可以使用监控仪表板的跨服务监控能力来监控数据流从源到[!DNL Identity Service]和[!DNL Profile]的旅程。

本教程提供了使用聚合监视视图和跨服务监视来监视数据流的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [数据流](../home.md):数据流是跨平台移动数据的数据作业的表示。跨不同的服务配置数据流，从而帮助将数据从源连接器移动到目标数据集、到[!DNL Identity]和[!DNL Profile]以及[!DNL Destinations]。
   * [数据流运行](../../sources/notifications.md):数据流运行是基于所选数据流的频率配置的循环计划作业。
* [来源](../../sources/home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [身份服务](../../identity-service/home.md):通过跨设备和系统连接身份，更好地视图个别客户及其行为。
* [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 汇总监控视图

在[平台UI](https://platform.adobe.com)中，从左侧导航中选择&#x200B;**[!UICONTROL Monitoring]**&#x200B;以访问[!UICONTROL Monitoring]仪表板。 [!UICONTROL Monitoring]仪表板包含有关所有源数据流的量度和信息，包括对从源到[!DNL Identity Service]和[!DNL Profile]的数据流量运行状况的洞察。

仪表板的中心是[!UICONTROL Source ingestion]面板，其中包含显示所摄取记录数据和记录失败的量度和图形。

![监控仪表板](../assets/ui/monitor-sources/monitoring-dashboard.png)

默认情况下，显示的数据包含过去24小时的摄取率。 选择&#x200B;**[!UICONTROL Last 24 hours]**&#x200B;以调整显示的记录的时间范围。

![change-date](../assets/ui/monitor-sources/change-date.png)

将显示一个日历弹出窗口，为您提供替代摄取时间框架的选项。 选择&#x200B;**[!UICONTROL Last 30 days]**，然后选择&#x200B;**[!UICONTROL Apply]**

![调整时间帧](../assets/ui/monitor-sources/adjust-timeframe.png)

图表默认处于启用状态，您可以禁用它们以展开下面源的列表。 选择&#x200B;**[!UICONTROL Metrics and graphs]**&#x200B;切换键以禁用图形。

![metrics-and-graphs](../assets/ui/monitor-sources/metrics-graphs.png)

| 源摄取 | 描述 |
| ---------------- | ----------- |
| [!UICONTROL Records ingested ] | 所摄取的记录总数。 |
| [!UICONTROL Records failed] | 由于数据中的错误而未收录的记录总数。 |
| [!UICONTROL Total failed dataflows] | 状态为`failed`的数据流的总数。 |

源摄取列表显示包含至少一个现有帐户的所有源。 该列表还包括有关每个源的摄取速率、失败记录数以及基于所应用时间帧的失败数据流总数的信息。

![源摄取](../assets/ui/monitor-sources/source-ingestion.png)

要对源的列表进行排序，请选择&#x200B;**[!UICONTROL My sources]**，然后从下拉菜单中选择所选类别。 例如，要关注云存储，请选择&#x200B;**[!UICONTROL Cloud storage]**

![按类别排序](../assets/ui/monitor-sources/sort-by-category.png)

要视图所有源中的所有现有数据流，请选择&#x200B;**[!UICONTROL Dataflows]**。

![视图全数据流](../assets/ui/monitor-sources/view-all-dataflows.png)

或者，您也可以在搜索栏中输入源以隔离单个源。 确定源后，请选择其旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png)以查看其活动数据流的列表。

![搜索](../assets/ui/monitor-sources/search.png)

出现一列表数据流。 要缩小列表并专注于存在错误的数据流，请选择&#x200B;**[!UICONTROL Show failures only]**。

![仅显示失败](../assets/ui/monitor-sources/show-failures-only.png)

找到要监视的数据流，然后选择其旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png)，以查看有关其运行状态的详细信息。

![数据流](../assets/ui/monitor-sources/dataflow.png)

数据流运行页显示有关数据流的运行开始日期、数据大小、状态及其处理时间持续时间的信息。 选择数据流运行开始时旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png)以查看其数据流运行详细信息。

![数据流运行开始](../assets/ui/monitor-sources/dataflow-run-start.png)

“[!UICONTROL Dataflow run details]”页显示有关数据流的元数据、部分摄取状态和错误摘要的信息。 错误摘要包含特定的顶级错误，该错误显示摄取过程在哪个步骤遇到错误。

向下滚动以查看有关所发生错误的更多特定信息。

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

[!UICONTROL Dataflow run errors]面板显示导致数据流摄取失败的特定错误和错误代码。 在此方案中，发生映射器转换错误，导致24条记录失败。

有关详细信息，请选择&#x200B;**[!UICONTROL Files]**。

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

[!UICONTROL Files]面板包含有关文件名称和路径的信息。

有关错误的更精细表示，请选择&#x200B;**[!UICONTROL Preview error diagnostics]**。

![文件](../assets/ui/monitor-sources/files.png)

出现[!UICONTROL Error diagnostics preview]窗口，在数据流中显示最多100个错误的预览。 您可以选择&#x200B;**[!UICONTROL Download]**&#x200B;以检索curl命令，然后该命令允许您下载错误诊断。

完成后，选择&#x200B;**[!UICONTROL Close]**

![错误诊断](../assets/ui/monitor-sources/error-diagnostics.png)

您可以使用顶部标题的痕迹导航系统导航回[!UICONTROL Monitoring]仪表板。 选择&#x200B;**[!UICONTROL Run start: 2/14/2021, 9:47 PM]**&#x200B;以返回到上一页，然后选择&#x200B;**[!UICONTROL Dataflow: Loyalty Data Ingestion Demo - Failed]**&#x200B;以返回到数据流页。

![痕迹](../assets/ui/monitor-sources/breadcrumbs.png)

## 跨服务监控

仪表板的上部包含从源级到[!DNL Identity Service]和[!DNL Profile]的摄取流的表示。 每个单元格都包含一个点标记，它指示在摄取阶段出现错误。 绿色圆点表示无错误摄取，而红色圆点表示在特定摄取阶段发生错误。

![跨服务监控](../assets/ui/monitor-sources/cross-service-monitoring.png)

在“数据流”页中，找到成功的数据流，并选择其旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png)以查看其数据流运行信息。

![数据流成功](../assets/ui/monitor-sources/dataflow-success.png)

[!UICONTROL Source ingestion]页包含确认成功获取数据流的信息。 从此处，您可以开始监控数据流从源级到[!DNL Identity Service]，然后到[!DNL Profile]的旅程。

选择&#x200B;**[!UICONTROL Identities]**&#x200B;可在[!UICONTROL Identities]阶段查看摄取。

![来源](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] 指标

[!UICONTROL Identity processing]页包含有关收录到[!DNL Identity Service]的记录的信息，包括添加的身份数、创建的图形和更新的图形。

选择数据流运行开始时旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png)，查看有关[!DNL Identity]数据流运行的详细信息。

![身份](../assets/ui/monitor-sources/identities.png)

| 身份量度 | 描述 |
| ---------------- | ----------- |
| [!UICONTROL Records received] | 从[!DNL Data Lake]收到的记录数。 |
| [!UICONTROL Records failed] | 由于数据中的错误而未引入平台的记录数。 |
| [!UICONTROL Records skipped] | 由于记录行中只有一个标识符，所以已摄取但未被收录到[!DNL Identity Service]中的记录数。 |
| [!UICONTROL Records ingested] | 收录到[!DNL Identity Service]中的记录数。 |
| [!UICONTROL Total records] | 所有记录（包括记录失败、已跳过记录、已添加[!DNL Identities]和已复制记录）的总计数。 |
| [!UICONTROL Identities added] | 添加到[!DNL Identity Service]的新标识符净数。 |
| [!UICONTROL Graphs created] | 在[!DNL Identity Service]中创建的净新标识图数。 |
| [!UICONTROL Graphs updated] | 使用新边缘更新的现有标识图的数量。 |
| [!UICONTROL Failed dataflow runs] | 失败的数据流运行数。 |
| [!UICONTROL Processing time] | 从摄取到完成的开始的时间戳。 |
| [!UICONTROL Status] | 定义数据流的整体状态。 可能的状态值为： <ul><li>`Success`:指示数据流处于活动状态，并正在根据提供的计划接收数据。</li><li>`Failed`:表示数据流的激活过程因错误而中断。 </li><li>`Processing`:指示数据流尚未处于活动状态。通常在创建新数据流后立即遇到此状态。</li></ul> |

[!UICONTROL Dataflow run details]页显示有关[!DNL Identity]数据流运行的详细信息，包括其IMS组织ID和数据流运行ID。 如果摄取过程中发生任何错误，此页还显示由[!DNL Identity Service]提供的相应错误代码和错误消息。

选择&#x200B;**[!UICONTROL Run start: 2/14/2021, 9:47 PM]**&#x200B;以返回到上一页。

![identities-dataflow run](../assets/ui/monitor-sources/identities-dataflow-run.png)

在[!UICONTROL Identity processing]页面中，选择&#x200B;**[!UICONTROL Profiles]**&#x200B;以查看[!UICONTROL Profiles]阶段中记录摄取的状态。

![select-用户档案](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] 指标

[!UICONTROL Profile processing]页包含有关收录到[!DNL Profile]的记录的信息，包括创建的用户档案片段数、更新的用户档案片段以及用户档案片段总数。

选择数据流运行开始时旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png)，查看有关[!DNL Profile]数据流运行的详细信息。

![用户档案](../assets/ui/monitor-sources/profiles.png)

| 用户档案量度 | 描述 |
| --------------- | ----------- |
| [!UICONTROL Records received] | 从[!DNL Data Lake]收到的记录数。 |
| [!UICONTROL Records failed ] | 由于错误而被收录但未被收录到[!DNL Profile]中的记录数。 |
| [!UICONTROL Profile fragments added] | 新[!DNL Profile]片段添加的净数。 |
| [!UICONTROL Profile fragments updated] | 已更新的现有[!DNL Profile]片段数 |
| [!UICONTROL Total Profile fragments] | 写入[!DNL Profile]的记录总数，包括所有已更新的[!DNL Profile]片段和新创建的[!DNL Profile]片段。 |
| [!UICONTROL Failed dataflow runs] | 失败的数据流运行数。 |
| [!UICONTROL Processing time] | 从摄取到完成的开始的时间戳。 |
| [!UICONTROL Status] | 定义数据流的整体状态。 可能的状态值为： <ul><li>`Success`:指示数据流处于活动状态，并正在根据提供的计划接收数据。</li><li>`Failed`:表示数据流的激活过程因错误而中断。 </li><li>`Processing`:指示数据流尚未处于活动状态。通常在创建新数据流后立即遇到此状态。</li></ul> |

[!UICONTROL Dataflow run details]页显示有关[!DNL Profile]数据流运行的详细信息，包括其IMS组织ID和数据流运行ID。 如果摄取过程中发生任何错误，此页还显示由[!DNL Profile]提供的相应错误代码和错误消息。

![用户档案-dataflow run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## 后续步骤

通过本教程，您使用&#x200B;**[!UICONTROL Monitoring]**&#x200B;仪表板成功监视了从源级到[!DNL Identity Service]和[!DNL Profile]的摄取数据流。 您还成功识别了导致数据流在摄取过程中失败的错误。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../profile/home.md)
* [数据科学工作区概述](../../data-science-workspace/home.md)
