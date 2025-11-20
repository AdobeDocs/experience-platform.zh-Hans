---
title: 监控流受众
description: 了解如何使用监控仪表板监控通过流式分段评估的受众
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 6%

---


# 监控流受众

简介模糊

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [数据流](../home.md)：数据流表示跨Experience Platform传输信息的数据作业。 它们可在各种服务中进行配置，以促进数据从源连接器移动到目标数据集以及Identity Service、Real-Time Customer Profile和Destinations。
* [分段服务](../../segmentation/home.md)：
* [能力](../../landing/license-usage-and-guardrails/capacity.md)：在Experience Platform中，能力让您知道您的组织是否超出了任何护栏，并为您提供如何解决这些问题的信息。

## 监控流式受众的量度 {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="评估率"
>abstract="此量度表示每秒计算的记录数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="P95 摄取延迟"
>abstract="此量度测量到达Adobe Experience Platform的事件的第95百分位延迟值，以成功评估受众。"
>text="Learn more in documentation"

下表提供了有关用于流受众的量度的更多详细信息。

| 量度 | 描述 | 维度 |
| ------ | ----------- | ---------- |
| 评估率 | 每秒处理的受众评估数。 | 沙盒，数据集 |
| P95 摄取延迟 | 成功事件到达受众的第95百分位延迟。 | 沙盒，数据集 |
| 已接收的记录 | 在所选时间窗口内从流式摄取接收的用于流式分段的记录总数。 | 数据集 |
| 评估的记录 | 在所选时间范围内，**成功**&#x200B;使用流式分段评估的记录总数。 | 数据集 |
| 失败的记录 | 由于所选时间范围内的错误而在流式分段中进行&#x200B;**失败**&#x200B;评估的记录总数。 | 数据集，流量运行 |
| 跳过的记录数 | 流分段中&#x200B;**跳过**&#x200B;评估的总记录数，原因是所选时间范围内的错误。 | 数据集，流量运行 |
| 配置文件符合条件 | 在所选时间范围内符合受众条件的配置文件数。 | 沙盒，受众 |
| 配置文件不合格 | 在所选时间范围内取消受众资格的用户档案数。 | 沙盒，受众 |

{style="table-layout:auto"}

## 使用流受众的监控功能板 {#monitoring-dashboard}

要访问流受众的监控仪表板，请转到Experience Platform UI，从左侧导航中选择&#x200B;**[!UICONTROL Monitoring]**，然后选择&#x200B;**[!UICONTROL Streaming end-to-end]**。

图像

仪表板顶部是&#x200B;**[!UICONTROL Audiences]**&#x200B;量度卡。 这会显示有关受众的&#x200B;**评估率**&#x200B;的信息。