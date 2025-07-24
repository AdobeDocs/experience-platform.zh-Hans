---
title: 监测流配置文件摄取
description: 了解如何使用监控仪表板监控流配置文件摄取
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---

# 监测流配置文件摄取

您可以使用Adobe Experience Platform UI中的监视仪表板实时监视组织中的流式配置文件摄取率。 使用此功能可以更好地透明流数据周围的吞吐量、延迟和数据质量指标。 此外，您可以使用此功能主动发出警报和检索可操作洞察，以确定潜在的容量违规和数据摄取问题。

请阅读以下指南，了解如何使用监视仪表板监视组织中流配置文件摄取作业的速率和量度。

## 了解流配置文件摄取仪表板

您可以在监视仪表板中使用三种不同的量度类别来流式处理配置文件摄取：[!UICONTROL 吞吐量]、[!UICONTROL 摄取]和[!UICONTROL 延迟]。

* **吞吐量**：选择&#x200B;**[!UICONTROL 吞吐量]**&#x200B;可查看有关Experience Platform在配置的时段内处理的数据量的信息。 请参阅此量度以评估系统的效率和容量。
   * **容量**：沙盒在定义的条件下可以处理的最大数据量。
   * **请求吞吐量**：摄取系统接收事件的速率（以每秒事件数衡量）。
   * **处理吞吐量**：系统成功摄取和处理传入事件负载的速率，以每秒事件数测量。
* **摄取**：选择[!UICONTROL 摄取]可查看有关沙盒中的摄取作业的信息。 这些引入作业使用三个不同的量度来衡量：
   * **创建的记录数**：在给定时间段内创建的记录总数。 此量度表示沙盒中成功的数据摄取流程。
   * **失败的记录**：由于错误而未引入的记录总数。
   * **删除的记录**：由于违反容量限制而被删除的记录总数。
* **延迟**：选择[!UICONTROL 延迟]可查看有关Experience Platform在给定时间段内响应请求或完成操作所花费时间的信息。

## 监控流式配置文件摄取的量度 {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="监测流配置文件摄取"
>abstract="流配置文件的监视仪表板显示有关吞吐量、摄取率和延迟的信息。 使用此功能板可查看、了解和分析数据处理量度。 ，即可将您的个人资料流式传输到Experience Platform。"
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
>title="P95摄取延迟"
>abstract="此量度测量从事件到抵达Experience Platform的那一刻到成功引入到配置文件存储区时的第95百分位延迟。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="最大吞吐量"
>abstract="此量度表示每秒进入流配置文件摄取的最大入站请求数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="已提取的记录"
>abstract="此量度表示在配置的时间范围内摄取到配置文件存储的总记录数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="失败的记录"
>abstract="此量度表示在配置的时间范围内，由于错误而未能摄取到配置文件存储中的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="跳过的记录数"
>abstract="此量度表示在配置的时间范围内由于配置或容量违规而丢弃的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="错误详细信息"
>abstract="此量度表示由于错误而失败的事件数。"
>text="Learn more in documentation"

| 量度 | 描述 | 维度 | 测量频率 |
| --- | --- | --- | --- |
| 请求吞吐量 | 此量度表示每秒进入摄取系统的事件数。 | 沙盒/数据流 | 实时监控，每60秒刷新一次数据。 |
| 处理吞吐量 | 此量度表示系统每秒成功摄取的事件数。 | 沙盒/数据流 | 实时监控，每60秒刷新一次数据。 |
| P95摄取延迟 | 此量度测量从事件到抵达Experience Platform的那一刻到成功引入到配置文件存储区时的第95百分位延迟。 | 沙盒/数据流 | 实时监控，每60秒刷新一次数据。 |
| 最大吞吐量 |
| 已提取的记录 | 此量度表示在配置的时间范围内摄取到配置文件存储的总记录数。 | <ul><li>沙盒/数据流</li><li>数据流运行</li></ul> | <ul><li>沙盒/数据流：实时监控，每60秒刷新一次数据。</li><li>数据流运行：15分钟后分组。</li></ul> |
| 失败的记录 | 此量度表示在配置的时间范围内，由于错误而未能摄取到配置文件存储中的记录总数。 | <ul><li>沙盒/数据流</li><li>数据流运行</li></ul> | <ul><li>沙盒/数据流：实时监控，每60秒刷新一次数据。</li><li>数据流运行：15分钟后分组。</li></ul> |
| 跳过的记录数 | 此量度表示在配置的时间范围内由于配置或容量违规而丢弃的记录总数。 | <ul><li>沙盒/数据流</li><li>数据流运行</li></ul> | <ul><li>沙盒/数据流：实时监控，每60秒刷新一次数据。</li><li>数据流运行：15分钟后分组。</li></ul> |
| 错误详细信息 | 此量度表示由于错误而失败的事件数。 | 数据流运行 | 按小时窗口分组。 |

{style="table-layout:auto"}