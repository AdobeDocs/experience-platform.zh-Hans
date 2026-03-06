---
title: 监控流式传输受众
description: 了解如何使用监控仪表板监控通过流分段评估的受众
hide: true
hidefromtoc: true
exl-id: b47325fb-7768-4bc0-92d2-5541729e636d
source-git-commit: 2d7ba15f918c314fe219212df82aec6d7ac1fc77
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 16%

---

# 监控流式传输受众

简介简介

## 快速入门

本指南要求您实际了解Experience Platform的以下组件：

* [数据流](../home.md)：数据流表示跨Experience Platform传输信息的数据作业。 它们被配置在不同的服务中，以促进数据从源连接器移动到目标数据集以及到身份服务、Real-Time Customer Profile和目标的移动。
* [分段服务](../../segmentation/home.md)：
* [容量](../../landing/license-usage-and-guardrails/capacity.md)：在Experience Platform方面，容量可以让您知道您的组织是否超过了任何防护栏，并为您提供了有关如何修复这些问题的信息。

## 流式受众监控量度 {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="评估率"
>abstract="此量度表示每秒评估的记录数量。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="P95 摄取延迟"
>abstract="此量度用于衡量事件到达 Adobe Experience Platform 后，成功评估并纳入受众所需延迟的第 95 百分位数。"
>text="Learn more in documentation"

下表提供了有关用于流受众的量度的更多详细信息。

| 量度 | 描述 | 维度 |
| ------ | ----------- | ---------- |
| 评估率 | 每秒处理的受众评估数。 | 沙箱，数据集 |
| P95 摄取延迟 | 活动成功到达观众的延迟的第95个百分点。 | 沙箱，数据集 |
| 已接收的记录 | 在所选时间窗口内从流式摄取接收的用于流式分段的记录总数。 | 数据集 |
| 已评估的记录 | 在所选时间窗口内，**使用流分段成功**&#x200B;评估的记录总数。 | 数据集 |
| 失败的记录 | 由于所选时间窗口内的错误而在流分段中&#x200B;**计算失败**&#x200B;的记录总数。 | 数据集，流运行 |
| 跳过的记录数 | 流分段中&#x200B;**跳过**&#x200B;评估的总记录数，原因是所选时间范围内的错误。 | 数据集，流量运行 |
| 配置文件符合条件 | 在所选时间范围内限定于受众的配置文件数。 | 沙盒，受众 |
| 配置文件不合格 | 在所选时间范围内取消受众资格的配置文件数。 | 沙盒，受众 |

{style="table-layout:auto"}

## 使用监视仪表板对访问群体进行流式传输 {#monitoring-dashboard}

要访问流式传输受众的监视仪表板，请转到Experience PlatformUI，从左侧导航中选择&#x200B;**[!UICONTROL Monitoring]**，然后选择&#x200B;**[!UICONTROL Streaming end-to-end]**。

图像

仪表板顶部是&#x200B;**[!UICONTROL Audiences]**&#x200B;量度卡。 这会显示有关受众的&#x200B;**评估率**&#x200B;的信息。
