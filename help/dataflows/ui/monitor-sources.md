---
keywords: Experience Platform；主页；热门主题；监视器帐户；监视器数据流；数据流；源
description: 本教程提供了使用聚合监视视图和跨服务监视来监视数据流的步骤。
solution: Experience Platform
title: 在UI中监控源的数据流
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 8%

---

# 在 UI 中监控源的数据流

>[!IMPORTANT]
>
>流源，如 [HTTP API源](../../sources/connectors/streaming/http.md) 监视仪表板当前不支持。 目前，您只能使用功能板监控批次源。

在Adobe Experience Platform中，数据从各种来源摄取，在Experience Platform中进行分析，并激活到各种目的地。 Platform通过提供数据流透明度，使跟踪这种潜在非线性数据流的过程更容易。

监视仪表板为您提供数据流历程的可视表示形式。 您可以使用聚合监控视图，从源级别垂直导航到数据流以及数据流运行，从而查看有助于数据流成功或失败的相应指标。 您还可以使用监视功能板的跨服务监视功能来监视数据流从源到目的地的历程。 [!DNL Identity Service]、和 [!DNL Profile].

本教程提供了使用聚合监视视图和跨服务监视来监视数据流的步骤。

## 快速入门 {#getting-started}

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [数据流](../home.md)：数据流表示跨Platform移动数据的数据作业。 数据流在不同的服务之间配置，有助于将数据从源连接器移动到目标数据集，以 [!DNL Identity] 和 [!DNL Profile]、和 [!DNL Destinations].
   * [数据流运行](../../sources/notifications.md)：数据流运行是基于所选数据流的频率配置的定期计划作业。
* [源](../../sources/home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [Identity Service](../../identity-service/home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
* [Real-time Customer Profile](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [沙盒](../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 汇总监控视图 {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="源提取"
>abstract="源提取视图包含有关数据湖服务中的数据活动状态和量度的信息，包括提取的记录和失败的记录。查看量度定义指南以了解有关量度和图表的更多信息。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="数据流运行详细信息"
>abstract="源处理包含有关数据湖服务中的数据活动状态和量度的信息，包括提取的记录和失败的记录。查看量度定义指南以了解有关量度和图表的更多信息。"
>text="Learn more in documentation"

在 [平台UI](https://platform.adobe.com)，选择 **[!UICONTROL 监控]** 从左侧导航访问 [!UICONTROL 监控] 仪表板。 此 [!UICONTROL 监控] 仪表板包含有关所有源数据流的量度和信息，包括对从源到的数据流量运行状况的分析 [!DNL Identity Service]、和 [!DNL Profile].

仪表板的中心是 [!UICONTROL 源摄取] 面板，其中包含量度和图形，用于显示有关已摄取记录和失败记录的数据。

![monitoring-dashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

默认情况下，显示的数据包含过去24小时的摄取率。 选择 **[!UICONTROL 最近24小时]** 以调整所显示记录的时间范围。

![change-date](../assets/ui/monitor-sources/change-date.png)

此时会出现一个日历弹出窗口，为您提供替代摄取时间范围的选项。 选择 **[!UICONTROL 最近30天]** 然后选择 **[!UICONTROL 应用]**

![调整时间范围](../assets/ui/monitor-sources/adjust-timeframe.png)

这些图形默认处于启用状态，您可以禁用它们以展开下面的源列表。 选择 **[!UICONTROL 量度和图形]** 切换可禁用图形。

![量度和图形](../assets/ui/monitor-sources/metrics-graphs.png)

| 源提取 | 描述 |
| ---------------- | ----------- |
| [!UICONTROL 已提取的记录] | 已摄取的记录总数。 |
| [!UICONTROL 失败的记录] | 由于数据错误而未提取的记录总数。 |
| [!UICONTROL 失败的数据流总数] | 具有的数据流总数 `failed` 状态。 |

源摄取列表显示至少包含一个现有帐户的所有源。 该列表还包括有关每个源的摄取率、失败记录的数量和基于您应用的时间范围的失败数据流总数量的信息。

![源摄取](../assets/ui/monitor-sources/source-ingestion.png)

要对源列表进行排序，请选择 **[!UICONTROL 我的源]** 然后从下拉菜单中选择您选择的类别。 例如，要侧重于云存储，请选择  **[!UICONTROL 云存储]**

![按类别排序](../assets/ui/monitor-sources/sort-by-category.png)

要查看所有源的所有现有数据流，请选择 **[!UICONTROL 数据流]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

或者，也可以在搜索栏中输入源以隔离单个源。 标识源后，选择过滤器图标 ![筛选](../assets/ui/monitor-sources/filter.png) 旁边会显示其活动数据流的列表。

![搜索](../assets/ui/monitor-sources/search.png)

此时将显示数据流列表。 要缩小列表范围并关注有错误的数据流，请选择 **[!UICONTROL 仅显示故障]**.

![仅显示故障](../assets/ui/monitor-sources/show-failures-only.png)

找到要监视的数据流，然后选择过滤器图标 ![筛选](../assets/ui/monitor-sources/filter.png) 在它旁边，查看有关其运行状态的更多信息。

![数据流](../assets/ui/monitor-sources/dataflow.png)

数据流运行页面显示有关数据流的运行开始日期、数据大小、状态及其处理持续时间的信息。 选择过滤器图标 ![筛选](../assets/ui/monitor-sources/filter.png) 位于数据流运行开始时间旁边，以查看其数据流运行详细信息。

![数据流 — 运行 — 启动](../assets/ui/monitor-sources/dataflow-run-start.png)

此 [!UICONTROL 数据流运行详细信息] 页面显示有关数据流元数据、部分摄取状态和错误摘要的信息。 错误摘要包含特定的顶级错误，该错误显示了摄取过程在哪个步骤遇到错误。

向下滚动查看有关所发生错误的更多具体信息。

![数据流 — 运行 — 详细信息](../assets/ui/monitor-sources/dataflow-run-details.png)

此 [!UICONTROL 数据流运行错误] 面板显示导致数据流摄取失败的特定错误和错误代码。 在此场景中，发生映射器转换错误，导致24条记录失败。

选择 **[!UICONTROL 文件]** 以了解更多信息。

![数据流运行错误](../assets/ui/monitor-sources/dataflow-run-errors.png)

此 [!UICONTROL 文件] 面板包含有关文件名和路径的信息。

要获得更细粒度的错误表示形式，请选择 **[!UICONTROL 预览错误诊断]**.

![文件](../assets/ui/monitor-sources/files.png)

此 [!UICONTROL 错误诊断预览] 此时将显示一个窗口，其中显示了数据流中多达100个错误的预览。 您可以选择 **[!UICONTROL 下载]** 检索curl命令，然后可下载错误诊断程序。

完成后，选择 **[!UICONTROL 关闭]**

![错误诊断](../assets/ui/monitor-sources/error-diagnostics.png)

您可以使用顶部标题的痕迹导航系统导航回 [!UICONTROL 监控] 仪表板。 选择 **[!UICONTROL 运行开始：2021年2月14日，晚上9:47]** 以返回上一页，然后选择 **[!UICONTROL 数据流：忠诚度数据摄取演示 — 失败]** 以返回数据流页面。

![痕迹导航](../assets/ui/monitor-sources/breadcrumbs.png)

## 后续步骤 {#next-steps}

通过学习本教程，您已使用成功地从源级别监视摄取数据流 **[!UICONTROL 监控]** 仪表板。 您还已成功识别出在摄取过程中导致数据流失败的错误。 有关更多详细信息，请参阅以下文档：

* [监视数据流中的身份](./monitor-identities.md)
* [监控数据流中的用户档案](./monitor-profiles.md)
