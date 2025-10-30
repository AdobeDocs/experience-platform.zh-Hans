---
title: 监控配置文件的流式摄取
description: 了解如何使用监控仪表板监控流配置文件摄取
exl-id: da7bb08d-2684-45a1-b666-7580f2383748
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 19%

---

# 监控配置文件的流式摄取

您可以使用Adobe Experience Platform UI中的监控仪表板对贵组织中的流式配置文件摄取进行实时监控。 使用此功能可访问与流数据相关的吞吐量、延迟和数据质量指标的更高透明度。 此外，使用此功能发出主动警报并检索可操作洞察，以帮助识别潜在的容量违规和数据摄取问题。

请阅读以下指南，了解如何使用监视仪表板跟踪组织中流配置文件摄取作业的速率和量度。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [数据流](../home.md)：数据流表示跨Experience Platform传输信息的数据作业。 它们可在各种服务中进行配置，以促进数据从源连接器移动到目标数据集以及Identity Service、Real-Time Customer Profile和Destinations。
* [实时客户个人资料](../../profile/home.md)： Real-Time Customer Profile将来自多个来源（在线、离线、CRM和第三方）的数据合并到每个客户的单个可操作视图中，从而实现跨所有接触点的一致且个性化的体验。
* [流式摄取](../../ingestion/streaming-ingestion/overview.md)：Experience Platform流式摄取为用户提供了一种方法，可实时将数据从客户端和服务器端设备发送到Experience Platform。Experience Platform允许您为每个客户生成实时客户档案，从而提供协调、一致和相关体验。&#x200B;AEM流式摄取在尽可能缩短延迟的情况下构建这些用户档案方面发挥着关键作用。
* [能力](../../landing/license-usage-and-guardrails/capacity.md)：在Experience Platform中，能力让您知道您的组织是否超出了任何护栏，并为您提供如何解决这些问题的信息。

>[!NOTE]
>
>流式处理吞吐量容量支持每秒多达1500个入站事件。 您可以购买额外的流分段以最多支持每秒13,500个额外的入站事件&#x200B;。 有关详细信息，请参阅[Real-Time CDP B2C Edition - Prime和Ultimate包产品说明](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)。

## 监控配置文件流式摄取的量度 {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="监控配置文件的流式摄取"
>abstract="流式处理配置文件的监控仪表板显示有关吞吐量、摄取率和延迟的信息。使用此仪表板查看、了解和分析数据处理量度。将您的流式处理配置文件导入 Experience Platform。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="请求吞吐量"
>abstract="此量度表示每秒进入摄取系统的事件数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="处理吞吐量"
>abstract="此量度表示系统每秒成功摄取的事件数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="P95 摄取延迟"
>abstract="此量度测量从某个事件到达 Experience Platform 到成功摄入配置文件存储区的第 95 个百分位数延迟。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="最大吞吐量"
>abstract="此量度表示每秒进入配置文件流式摄取的最大入站请求数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="已提取的记录"
>abstract="此量度表示在某个已配置的时间窗口内摄入配置文件存储区的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="失败的记录"
>abstract="此量度表示在某个已配置的时间窗口内由于出错而未能摄入配置文件存储区的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="跳过的记录数"
>abstract="此量度表示在某个已配置的时间窗口内由于配置或容量违规而被丢失的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="错误详细信息"
>abstract="此量度表示由于出错而失败的事件数。"
>text="Learn more in documentation"

可使用量度表获取特定于您的数据流的信息。 有关每列的详细信息，请参阅下表。

| 量度 | 描述 | 维度 | 测量频率 |
| --- | --- | --- | --- |
| 请求吞吐量 | 此量度表示每秒进入摄取系统的事件数。 | 沙盒/数据流 | 实时监控，每60秒刷新一次数据。 |
| 处理吞吐量 | 此量度表示系统每秒成功摄取的事件数。 | 沙盒/数据流 | 实时监控，每60秒刷新一次数据。 |
| P95 摄取延迟 | 此量度测量从某个事件到达 Experience Platform 到成功摄入配置文件存储区的第 95 个百分位数延迟。 | 沙盒/数据流 | 实时监控，每60秒刷新一次数据。 |
| 最大吞吐量 | 此量度表示每秒进入流配置文件摄取的最大入站请求数 | <ul><li>沙盒/数据流</li><li>数据流运行</li></ul> |  |
| 已提取的记录 | 此量度表示在某个已配置的时间窗口内摄入配置文件存储区的记录总数。 | <ul><li>沙盒/数据流</li><li>数据流运行</li></ul> | <ul><li>沙盒/数据流：实时监控，每60秒刷新一次数据。</li><li>数据流运行：15分钟后分组。</li></ul> |
| 失败的记录 | 此量度表示在某个已配置的时间窗口内由于出错而未能摄入配置文件存储区的记录总数。 | <ul><li>沙盒/数据流</li><li>数据流运行</li></ul> | <ul><li>沙盒/数据流：实时监控，每60秒刷新一次数据。</li><li>数据流运行：15分钟后分组。</li></ul> |
| 跳过的记录数 | 此量度表示在某个已配置的时间窗口内由于配置或容量违规而被丢失的记录总数。 | <ul><li>沙盒/数据流</li><li>数据流运行</li></ul> | <ul><li>沙盒/数据流：实时监控，每60秒刷新一次数据。</li><li>数据流运行：15分钟后分组。</li></ul> |
| 错误详细信息 | 此量度表示由于出错而失败的事件数。 | 数据流运行 | 按小时窗口分组。 |

{style="table-layout:auto"}

## 使用监视仪表板进行流式处理配置文件摄取

要访问流配置文件摄取的监视仪表板，请转到Experience Platform UI，从左侧导航中选择&#x200B;**[!UICONTROL Monitoring]**，然后选择&#x200B;**[!UICONTROL Streaming end-to-end]**。

![用于流式处理配置文件摄取的监视仪表板。](../assets/ui/streaming-profiles/monitoring-dashboard.png)

请参阅&#x200B;*[!UICONTROL Profile]*&#x200B;量度卡片的仪表板顶部标题。 使用此显示可查看有关已摄取、失败和跳过的记录的信息，以及有关请求吞吐量和延迟的当前状态的信息。

![个人资料卡。](../assets/ui/streaming-profiles/profile-card.png)

接下来，使用界面查看有关流配置文件摄取量度的详细信息。 使用日历功能在不同的时间范围之间进行切换。 您可以从以下预配置的时间窗口中选择：

* [!UICONTROL Last 6 hours]
* [!UICONTROL Last 12 hours]
* [!UICONTROL Last 24 hours]
* [!UICONTROL Last 7 days]
* [!UICONTROL Last 30 days]

或者，您可以使用日历手动配置自己的时间范围。

您可以在监视仪表板中使用三个不同的量度类别来流式处理配置文件摄取： [!UICONTROL Throughput]、[!UICONTROL Ingestion]和[!UICONTROL Latency]。

>[!BEGINTABS]

>[!TAB 吞吐量]

选择&#x200B;**[!UICONTROL Throughput]**&#x200B;可查看有关Experience Platform在配置的时间段内正在处理的数据量的信息。 请参阅此量度以评估系统的效率和容量。

![显示设置为“吞吐量”的仪表板。](../assets/ui/streaming-profiles/throughput.png)

* **[容量](../../landing/license-usage-and-guardrails/capacity.md)**：沙盒在定义的条件下可以处理的最大数据量。
* **请求吞吐量**：摄取系统接收事件的速率（以每秒事件数衡量）。
* **处理吞吐量**：系统成功摄取和处理传入事件负载的速率，以每秒事件数测量。

>[!TAB 引入]

**摄取**：选择&#x200B;**[!UICONTROL Ingestion]**&#x200B;可查看有关沙盒中的摄取作业的信息。 这些摄取作业通过三个不同的指标进行测量。

![显示设置为“摄取”的仪表板。](../assets/ui/streaming-profiles/ingestion.png)

* **已摄取的记录**：在给定时间段内创建的记录总数。 此量度表示沙盒中成功的数据摄取流程。
* **跳过的记录数**：由于错误而未引入的记录总数。
* **跳过的记录数**：由于违反容量限制而被丢弃的记录总数。

>[!TAB 延迟]

选择&#x200B;**[!UICONTROL Latency]**&#x200B;可查看有关Experience Platform在给定时间段内响应请求或完成操作所花费时间的信息。

![显示设置为“延迟”的仪表板。](../assets/ui/streaming-profiles/latency.png)

>[!ENDTABS]

### 使用数据流量度表

数据流表列出了所有流式摄取活动及其对应的实时客户资料量度集。 每个数据流都与其对应的数据集一起列出。

如果您即将达到沙盒级别的容量限制，则可以参考[!UICONTROL Max throughput]列以识别任何对您的使用率有贡献的现有数据流。 有关数据流管理最佳实践的更多信息，请阅读[最佳实践部分](#best-practices)。

要监视特定数据流中摄取的数据，请选择数据流名称旁边的过滤器图标![过滤器](/help/images/icons/filter-add.png)。

![量度页面](../assets/ui/streaming-profiles/metrics.png)

接下来，使用数据流指标界面选择要检查的特定流运行。 选择流运行迭代旁边的过滤器图标![过滤器](/help/images/icons/filter-add.png)以查看选定流运行的特定量度。

![数据流指标接口。](../assets/ui/streaming-profiles/flows.png)

数据流运行代表数据流执行的实例。 例如，如果数据流计划在上午9:00、上午10:00和上午11:00每小时运行，则您将运行三个流实例。 流量运行特定于您的特定组织。

使用数据流运行详细信息页面可查看所选运行迭代的量度和信息。

![数据流运行活动接口。](../assets/ui/streaming-profiles/flow-runs.png)

## 数据流管理最佳实践 {#best-practices}

有关如何在Experience Platform上以最佳方式管理数据流和优化数据消耗的信息，请阅读以下部分。

### 评估和优化流摄取数据流

为了确保高效的流式摄取，请审查和调整数据流和处理策略：

* **评估当前使用情况**：确定哪些数据流和数据集对吞吐量的贡献最大。
* **优先处理有价值的数据**：并非所有数据都是必需的。 排除不支持您的用例的数据，以减少存储并提高效率。
* **优化处理模式**：确定是否可以将某些数据从流式转移到批量摄取。 保留流以供需要低延迟的用例使用，例如实时分段。

### 规划容量和季节性流量

如果当前每秒&#x200B;**1,500个事件的限制**&#x200B;不足，请考虑优化数据策略或增加许可证容量：

* **分析数据集和沙盒使用情况**：查看当前和历史数据以了解流量和参与如何影响流式分段吞吐量。
* **考虑季节性**：识别由周期性营销活动或特定于行业的周期驱动的峰值流量时段。
* **预测未来需求**：根据过去的季节性趋势、计划的促销活动或主要事件来估计即将到来的流量和参与量。

| 促成因素 | 内容 | 对用例的影响 | 最佳实践 |
| --- | --- | --- | --- |
| 批量到流式转换 | 批量工作负载转换为流式传输会显着增加吞吐量，从而影响性能和资源分配。 例如，在没有速率限制的事件后执行批量配置文件更新。 | 当不需要低延迟处理时，无需对批量用例使用流策略。 | 评估用例要求。 对于批量出站营销，请考虑使用[批量摄取](../../ingestion/batch-ingestion/overview.md)而不是流式处理来更有效地管理数据摄取。 |
| 不必要的数据摄取 | 引入个性化不需要的数据可在不增加价值的情况下增加吞吐量，从而浪费资源。 例如，无论相关性如何，都将所有Analytics流量摄取到用户档案中。 | 过多的不相关数据会产生噪音，使得识别有影响的数据点变得更困难。 在定义和管理受众和用户档案时，这也会造成摩擦。 | 仅摄取用例所需的数据。 确保过滤掉不必要的数据。<ul><li>**Adobe Analytics**：使用[行级筛选](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile)优化数据摄取。</li><li>**源**：使用[[!DNL Flow Service] API为支持的源（如](../../sources/tutorials/api/filter.md)和[!DNL Snowflake]）筛选行级数据[!DNL Google BigQuery]。</li></li>**Edge数据流**：配置[动态数据流](../../datastreams/configure-dynamic-datastream.md)以对来自WebSDK的流量执行行级筛选。</li></ul> |

{style="table-layout:auto"}

### 常见问题解答 {#faq}

请阅读此部分，了解有关监控流配置文件摄取的常见问题解答。

#### 为什么我的量度在容量功能板和监控功能板之间在请求吞吐量方面看起来不同？

+++回答

[!UICONTROL Monitoring]仪表板显示用于摄取和处理的实时量度。 这些数字是在活动时记录的准确量度。 相反，[!UICONTROL Capacity]仪表板使用平滑机制来计算吞吐量容量。 此机制有助于减少短暂的尖峰，使其不再立即被认定为违规，并确保容量警报侧重于持续趋势，而不是短暂的突发事件。

由于平滑机制，您可能会注意到：

* 未出现在[!UICONTROL Monitoring]中的[!UICONTROL Capacity]的小峰值。
* [!UICONTROL Capacity]中的值比相同时间戳的[!UICONTROL Monitoring]略低。

这两个功能板虽然准确无误，但其设计目的却不尽相同。

* [!UICONTROL Monitoring]：详细的逐刻操作可见性。
* [!UICONTROL Capacity]：用于标识使用和违规模式的策略视图。

+++

## 后续步骤 {#next-steps}

通过学习本教程，您已了解如何监控组织中的流式配置文件引入作业。 请阅读以下文档，了解有关监控Real-time Customer Profile数据的更多信息。

* [使用监视仪表板](./monitor.md)。
* [监视配置文件数据](./monitor-profiles.md)。
