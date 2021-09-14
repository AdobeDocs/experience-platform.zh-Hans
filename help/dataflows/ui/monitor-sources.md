---
keywords: Experience Platform；主页；热门主题；监视帐户；监视数据流；数据流；源
description: 本教程提供了使用聚合监控视图和跨服务监控来监控数据流的步骤。
solution: Experience Platform
title: 在UI中监视源的数据流
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: a5b52d7cc2a39ce15b5a9568df14c86624ae069a
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# 在UI中监视源的数据流

>[!IMPORTANT]
>
>监视功能板当前不支持流源，如[HTTP API源](../../sources/connectors/streaming/http.md)。 此时，您只能使用功能板来监控批量源。

在Adobe Experience Platform中，从各种来源摄取数据，在Experience Platform内进行分析，并激活到各种不同的目标。 Platform通过提供数据流的透明度，使跟踪这种潜在的非线性数据流的过程变得更加容易。

监控仪表板可直观地呈现数据流的历程。 您可以使用聚合监视视图，并从源级别垂直导航到数据流，以及到数据流运行，从而允许您查看对数据流成功或失败有贡献的相应量度。 您还可以使用监控仪表板的跨服务监控容量来监控数据流从源到[!DNL Identity Service]和[!DNL Profile]的历程。

本教程提供了使用聚合监控视图和跨服务监控来监控数据流的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [数据流](../home.md):数据流是跨平台移动数据的数据作业的表示形式。数据流是跨不同的服务配置的，有助于将数据从源连接器移动到目标数据集，移动到[!DNL Identity]和[!DNL Profile]，以及[!DNL Destinations]。
   * [数据流运行](../../sources/notifications.md):数据流运行是基于所选数据流的频率配置的定期计划作业。
* [来源](../../sources/home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [Identity服务](../../identity-service/home.md):通过跨设备和系统桥接身份，更好地了解各个客户及其行为。
* [实时客户资料](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [沙盒](../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 汇总监控视图

在[Platform UI](https://platform.adobe.com)中，从左侧导航中选择&#x200B;**[!UICONTROL Monitoring]**&#x200B;以访问[!UICONTROL Monitoring]功能板。 [!UICONTROL 监视]功能板包含有关所有源数据流的量度和信息，包括对从源到[!DNL Identity Service]和[!DNL Profile]的数据流量运行状况的分析。

功能板的中心是[!UICONTROL 源摄取]面板，其中包含显示所摄取记录数据和记录失败的量度和图形。

![监控仪表板](../assets/ui/monitor-sources/monitoring-dashboard.png)

默认情况下，显示的数据包含过去24小时的摄取率。 选择&#x200B;**[!UICONTROL 最近24小时]**&#x200B;以调整显示的记录的时间范围。

![更改日期](../assets/ui/monitor-sources/change-date.png)

此时会出现日历弹出窗口，为您提供替代摄取时间范围的选项。 选择&#x200B;**[!UICONTROL 最近30天]**，然后选择&#x200B;**[!UICONTROL 应用]**

![调整时间范围](../assets/ui/monitor-sources/adjust-timeframe.png)

图表默认处于启用状态，您可以禁用它们以展开下面的源列表。 选择&#x200B;**[!UICONTROL 量度和图形]**&#x200B;切换开关以禁用图形。

![量度和图形](../assets/ui/monitor-sources/metrics-graphs.png)

| 源摄取 | 描述 |
| ---------------- | ----------- |
| [!UICONTROL 摄取的记录  ] | 摄取的记录总数。 |
| [!UICONTROL 记录失败] | 由于数据中的错误而未摄取的记录总数。 |
| [!UICONTROL 失败的数据流总数] | 状态为`failed`的数据流总数。 |

源摄取列表显示至少包含一个现有帐户的所有源。 该列表还包含有关每个源的摄取率、失败记录数以及基于所应用时间范围的失败数据流总数的信息。

![源摄取](../assets/ui/monitor-sources/source-ingestion.png)

要对源列表进行排序，请选择&#x200B;**[!UICONTROL My sources]**，然后从下拉菜单中选择您选择的类别。 例如，要重点关注云存储，请选择&#x200B;**[!UICONTROL 云存储]**

![按类别排序](../assets/ui/monitor-sources/sort-by-category.png)

要查看所有源中的所有现有数据流，请选择&#x200B;**[!UICONTROL 数据流]**。

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

或者，您也可以在搜索栏中输入源以隔离单个源。 识别源后，请选择其旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png) ，以查看其活动数据流的列表。

![搜索](../assets/ui/monitor-sources/search.png)

此时将显示数据流列表。 要缩小列表范围并重点关注出错的数据流，请选择&#x200B;**[!UICONTROL 仅显示失败]**。

![仅显示失败](../assets/ui/monitor-sources/show-failures-only.png)

找到要监视的数据流，然后选择其旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png) ，以查看有关其运行状态的更多信息。

![数据流](../assets/ui/monitor-sources/dataflow.png)

“数据流运行”页显示有关数据流运行开始日期、数据大小、状态及其处理时间的信息。 选择数据流运行开始时间旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png) ，以查看其数据流运行详细信息。

![数据流运行启动](../assets/ui/monitor-sources/dataflow-run-start.png)

[!UICONTROL 数据流运行详细信息]页显示有关数据流元数据、部分摄取状态和错误摘要的信息。 错误摘要包含特定的顶级错误，该错误会显示摄取流程在哪个步骤遇到错误。

向下滚动以查看有关所发生错误的更多特定信息。

![数据流运行详细信息](../assets/ui/monitor-sources/dataflow-run-details.png)

[!UICONTROL 数据流运行错误]面板显示导致数据流摄取失败的特定错误和错误代码。 在这种情况下，发生映射器转换错误，导致24条记录失败。

选择&#x200B;**[!UICONTROL 文件]**&#x200B;以了解更多信息。

![数据流运行错误](../assets/ui/monitor-sources/dataflow-run-errors.png)

[!UICONTROL 文件]面板包含有关文件名和路径的信息。

有关错误的更详细表示，请选择&#x200B;**[!UICONTROL 预览错误诊断]**。

![文件](../assets/ui/monitor-sources/files.png)

出现[!UICONTROL 错误诊断预览]窗口，显示数据流中最多100个错误的预览。 您可以选择&#x200B;**[!UICONTROL Download]**&#x200B;以检索curl命令，然后该命令允许您下载错误诊断。

完成后，选择&#x200B;**[!UICONTROL Close]**

![错误诊断](../assets/ui/monitor-sources/error-diagnostics.png)

您可以使用顶部标题的痕迹导航系统导航回[!UICONTROL 监视]功能板。 选择&#x200B;**[!UICONTROL 运行开始：2/14/2021, 9:47 PM]**&#x200B;返回到上一页，然后选择&#x200B;**[!UICONTROL 数据流：忠诚度数据摄取演示 — 未能]**&#x200B;返回到数据流页面。

![痕迹导航](../assets/ui/monitor-sources/breadcrumbs.png)

## 跨服务监控

功能板的上半部分包含从源级别到[!DNL Identity Service]和[!DNL Profile]的摄取流的表示形式。 每个单元格都包含一个圆点标记，用于指示在摄取阶段出现错误的情况。 绿色圆点表示无错误摄取，而红色圆点表示在特定摄取阶段发生错误。

![跨服务监控](../assets/ui/monitor-sources/cross-service-monitoring.png)

在数据流页面中，找到成功的数据流，并选择其旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png) ，以查看其数据流运行信息。

![数据流成功](../assets/ui/monitor-sources/dataflow-success.png)

[!UICONTROL 源摄取]页包含确认数据流是否成功摄取的信息。 从此处，您可以开始监控数据流从源级到[!DNL Identity Service]的历程，然后再到[!DNL Profile]的历程。

选择&#x200B;**[!UICONTROL 标识]**&#x200B;以在[!UICONTROL 标识]阶段查看摄取。

![来源](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] 量度

[!UICONTROL 身份处理]页面包含有关摄取到[!DNL Identity Service]的记录的信息，包括添加的身份数、创建的图表和更新的图表。

选择数据流运行开始时间旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png) ，以查看有关[!DNL Identity]数据流运行的更多信息。

![标识](../assets/ui/monitor-sources/identities.png)

| 身份量度 | 描述 |
| ---------------- | ----------- |
| [!UICONTROL 收到的记录] | 从[!DNL Data Lake]收到的记录数。 |
| [!UICONTROL 记录失败] | 由于数据中的错误而未摄取到平台中的记录数。 |
| [!UICONTROL 跳过的记录数] | 被摄取但未被摄取到[!DNL Identity Service]中的记录数，因为记录行中只有一个标识符。 |
| [!UICONTROL 摄取的记录] | 摄取到[!DNL Identity Service]中的记录数。 |
| [!UICONTROL 记录总数] | 所有记录（包括失败的记录、跳过的记录、添加的[!DNL Identities]和重复记录）的总计数。 |
| [!UICONTROL 添加了身份] | 添加到[!DNL Identity Service]的新标识符净数。 |
| [!UICONTROL 创建的图形] | 在[!DNL Identity Service]中创建的新身份图的净数量。 |
| [!UICONTROL 更新的图表] | 使用新边缘更新的现有身份图的数量。 |
| [!UICONTROL 数据流运行失败] | 失败的数据流运行数。 |
| [!UICONTROL 处理时间] | 从摄取开始到完成的时间戳。 |
| [!UICONTROL 状态] | 定义数据流的整体状态。 可能的状态值包括： <ul><li>`Success`:表示数据流处于活动状态，并正在根据提供的计划摄取数据。</li><li>`Failed`:表示数据流的激活过程因错误而中断。 </li><li>`Processing`:表示数据流尚未处于活动状态。此状态通常会在创建新数据流后立即出现。</li></ul> |

“[!UICONTROL 数据流运行详细信息]”页显示有关[!DNL Identity]数据流运行的更多信息，包括其IMS组织ID和数据流运行ID。 如果摄取过程中发生任何错误，此页面还会显示由[!DNL Identity Service]提供的相应错误代码和错误消息。

选择&#x200B;**[!UICONTROL 运行开始：2/14/2021, 9:47 PM]**&#x200B;返回到上一页。

![identities-dataflow run](../assets/ui/monitor-sources/identities-dataflow-run.png)

从[!UICONTROL 身份处理]页面中，选择&#x200B;**[!UICONTROL Profiles]**&#x200B;以查看[!UICONTROL Profiles]阶段中记录摄取的状态。

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] 量度

[!UICONTROL 配置文件处理]页包含有关摄取到[!DNL Profile]的记录的信息，包括创建的配置文件片段数、更新的配置文件片段数以及配置文件片段总数。

选择数据流运行开始时间旁边的过滤器图标![filter](../assets/ui/monitor-sources/filter.png) ，以查看有关[!DNL Profile]数据流运行的更多信息。

![用户档案](../assets/ui/monitor-sources/profiles.png)

| 配置文件量度 | 描述 |
| --------------- | ----------- |
| [!UICONTROL 收到的记录] | 从[!DNL Data Lake]收到的记录数。 |
| [!UICONTROL 记录失败  ] | 由于错误而被摄取但未被摄取到[!DNL Profile]中的记录数。 |
| [!UICONTROL 添加了配置文件片段] | 新增的[!DNL Profile]片段的净数。 |
| [!UICONTROL 更新了配置文件片段] | 更新的现有[!DNL Profile]片段数 |
| [!UICONTROL 配置文件片段总数] | 写入[!DNL Profile]的记录总数，包括所有已更新的现有[!DNL Profile]片段和已创建的新[!DNL Profile]片段。 |
| [!UICONTROL 数据流运行失败] | 失败的数据流运行数。 |
| [!UICONTROL 处理时间] | 从摄取开始到完成的时间戳。 |
| [!UICONTROL 状态] | 定义数据流的整体状态。 可能的状态值包括： <ul><li>`Success`:表示数据流处于活动状态，并正在根据提供的计划摄取数据。</li><li>`Failed`:表示数据流的激活过程因错误而中断。 </li><li>`Processing`:表示数据流尚未处于活动状态。此状态通常会在创建新数据流后立即出现。</li></ul> |

“[!UICONTROL 数据流运行详细信息]”页显示有关[!DNL Profile]数据流运行的更多信息，包括其IMS组织ID和数据流运行ID。 如果摄取过程中发生任何错误，此页面还会显示由[!DNL Profile]提供的相应错误代码和错误消息。

![profiles-dataflow运行](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## 后续步骤

通过本教程，您已使用&#x200B;**[!UICONTROL 监控]**&#x200B;功能板成功监控了从源级、[!DNL Identity Service]和[!DNL Profile]的摄取数据流。 您还成功识别了在摄取过程中导致数据流失败的错误。 有关更多详细信息，请参阅以下文档：

* [实时客户资料概述](../../profile/home.md)
* [数据科学工作区概述](../../data-science-workspace/home.md)
