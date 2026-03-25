---
title: 监测边缘分段
description: 了解如何使用监控仪表板来观察边缘分段吞吐量。
source-git-commit: 809f80c721d6eedf5ee88dbb1cf4bf7e5a413614
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---


# 监测边缘分段

您可以使用Adobe Experience Platform UI中的监控仪表板对贵组织中的边缘分段进行实时监控。 使用此功能可以提高边缘数据吞吐量的透明度。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [数据流](../../datastreams/overview.md)：数据流允许您将Experience Platform Edge Network连接到数据集。
* [能力](../../landing/license-usage-and-guardrails/capacity.md)：在Experience Platform中，能力让您知道您的组织是否超出了任何护栏，并为您提供如何解决这些问题的信息。
* [Edge分段](../../segmentation/methods/edge-segmentation.md)： Edge分段可在[边缘即时评估Adobe Experience Platform中的区段定义，从而启用同一页面和下一页面个性化用例。](../../landing/edge-and-hub-comparison.md)

## 访问 {#access}

要访问边缘分段吞吐量的监视仪表板，请在&#x200B;**[!UICONTROL Monitoring]**&#x200B;部分中选择&#x200B;**[!UICONTROL Data management]**，然后选择&#x200B;**[!UICONTROL Edge]**。

![访问监视器边缘分段仪表板的方法已突出显示。](/help/dataflows/assets/ui/monitor-edge/access.png)

此时将显示监视仪表板。 其中显示了边缘流吞吐量的监控量度、显示边缘流吞吐量的速率的图形以及数据流视图。 这些量度可以按服务、边缘和日期进行过滤。

![监视仪表板中的筛选选项突出显示。](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>如果选择&#x200B;**，则只能看到数据流视图** 1。[!UICONTROL Edge segmentation throughput]

如果按服务过滤，则可以选择要查看其吞吐量信息的服务。 其中包括Edge分段、数据收集、Target、Adobe Journey Optimizer、Offer Decisioning、自定义个性化目标、事件转发、Adobe Analytics和Adobe Audience Manager等服务。

如果按边过滤，则可以选择要查看有关哪个边的信息。 受支持的边缘包括美国东岸、美国西岸、欧洲、印度、新加坡、澳大利亚、日本和瑞士。 可一次选取多个要查看的边。

如果按日期过滤，则可以选择用于过滤事件的时间范围。 此时间刻度最多可设置30天。 或者，您可以使用以下预配置的时间刻度之一： [!UICONTROL Last 6 hours]、[!UICONTROL Last 12 hours]、[!UICONTROL Last 24 hours]、[!UICONTROL Last 7 days]和[!UICONTROL Last 30 days]。

## 监控边缘吞吐量的量度

度量表提供特定于所选服务的边缘吞吐量的信息。 有关每一列的详细信息，请参见下表。

| 量度 | 描述 |
| ------ | ----------- |
| 请求已收到 | 时间范围内所选边缘接收的请求数。 |
| 峰值吞吐量 | 时间范围内所选边缘接收请求的最高速率。 |

{style="table-layout:auto"}

## 边缘分段吞吐量的监控图

监控图显示在分配的时间范围内选定边缘每秒接收的记录数，与允许的最大容量相比。

![显示边缘分段吞吐量图。](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## 数据流视图

>[!NOTE]
>
>如果要筛选Edge分段吞吐量，则数据流视图仅&#x200B;**可用**。

数据流视图部分显示通过沙盒边缘的最新数据流列表。

![将显示数据流视图，显示有关列出的数据流的信息。](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| 字段 | 描述 |
| ----- | ----------- |
| 数据流名称 | 数据流的名称。 |
| 数据集 | 数据流所属的数据集的名称。 |
| 服务已启用 | 为数据流启用的服务的名称。 |
| 请求 | 通过数据流的请求数。 |
| 峰值吞吐量 | 通过数据流的最大请求速率。 |
