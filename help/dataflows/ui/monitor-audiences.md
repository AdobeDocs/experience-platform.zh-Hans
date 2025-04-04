---
description: 了解如何使用Experience Platform用户界面在分段期间监测数据流。
title: 在UI中监控受众的数据流
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 4%

---

# 在UI中监控受众的数据流

分段服务允许您通过[!DNL Real-Time Customer Profile]数据的区段定义或其他来源创建受众。 Experience Platform提供数据流，用于透明地跟踪从源到目标的这种数据流。

使用监视仪表板可查看受众中数据活动的可视表示形式，包括数据分段的状态。 阅读教程，了解如何使用监视仪表板通过Experience Platform用户界面监视数据分段，从而跟踪受众激活、评估和导出作业的状态。

## 快速入门 {#getting-started}

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

- [数据流](../home.md)：数据流是跨Experience Platform移动数据的数据作业的表示形式。 数据流在不同服务之间配置，帮助将数据从源连接器移动到目标数据集、[!DNL Identity]和[!DNL Profile]以及[!DNL Destinations]。
   - [数据流运行](../../sources/notifications.md)：数据流运行是基于所选数据流的频率配置的周期性计划作业。
- [分段](../../segmentation/home.md)：分段允许您根据实时客户档案数据创建受众。
   - [激活作业](../../destinations/ui/activation-overview.md)：激活作业用于将受众激活到指定的目标。
   - [评估作业](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment)：评估作业是评估受众的异步进程。
   - [导出作业](../../segmentation/api/export-jobs.md)：导出作业是用于将受众成员保留到数据集的异步进程。
- [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 监控受众仪表板 {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="受众"
>abstract="受众视图包含有关您的组织的所有受众的信息，以及有关其激活和评估作业的更多信息。"

要访问&#x200B;**[!UICONTROL 受众]**&#x200B;仪表板，请在左侧导航中选择&#x200B;**[!UICONTROL 监控]**。 在&#x200B;**[!UICONTROL 监控]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 受众]**&#x200B;信息卡。

![受众卡。 显示有关上一个评估作业和上一个导出作业的信息。](../assets/ui/monitor-audiences/audience-card.png)

在主&#x200B;**[!UICONTROL 受众]**&#x200B;仪表板上，**[!UICONTROL 受众]**&#x200B;信息卡显示上次评估作业和上次导出作业的状态和日期。

仪表板本身包含受众和分段作业的量度。 默认情况下，仪表板显示过去24小时的受众量度。 要了解有关分段作业视图的更多信息，请阅读[监视分段作业](#monitoring-segmentation-jobs-dashboard)部分。

>[!IMPORTANT]
>
>目前，监控受众仪表板仅支持激活到[批处理（基于文件）目标](../../destinations/destination-types.md#file-based)的受众。

![受众仪表板。 显示有关组织和沙盒中不同受众的信息。](../assets/ui/monitor-audiences/audience-dashboard.png)

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| ------ | ----------- |
| **[!UICONTROL 受众名称]** | 受众的名称。 |
| **[!UICONTROL 数据类型]** | 受众的数据类型。 可能的值包括&#x200B;**[!UICONTROL 客户]**、**[!UICONTROL 帐户]**&#x200B;和&#x200B;**[!UICONTROL 潜在客户]**。 您可以使用卡片功能区上方的[!UICONTROL 数据类型]筛选器查看指定数据类型的受众。 |
| **[!UICONTROL 上次评估时间戳]** | 受众最后一次评估作业运行的日期和时间。 |
| **[!UICONTROL 上次评估状态]** | 受众上次评估作业的状态。 可能的值包括&#x200B;**[!UICONTROL 成功]**、**[!UICONTROL 没有运行]**&#x200B;和&#x200B;**[!UICONTROL 失败]**。 |
| **[!UICONTROL 上次评估方法]** | 受众的评估方法。 由于仅支持批次分段，因此唯一可能的值为&#x200B;**[!UICONTROL 批次]**。 |
| **[!UICONTROL 上次评估配置文件]** | 在受众的上次评估作业中评估的用户档案数。 |
| **[!UICONTROL 上次激活时间戳]** | 受众最后一次激活作业运行的日期和时间。 |
| **[!UICONTROL 上次激活状态]** | 受众最后一次激活作业的状态。 可能的值包括&#x200B;**[!UICONTROL 成功]**、**[!UICONTROL 没有运行]**&#x200B;和&#x200B;**[!UICONTROL 失败]**。 |
| **[!UICONTROL 上次激活身份]** | 在受众的上次激活作业中激活的身份数。 |
| **[!UICONTROL 上次激活目标]** | 受众的上次激活作业激活到的目标的名称。 |

您可以通过选择过滤器图标（![过滤器图标）来将结果过滤到特定受众，并查看其分段作业。](/help/images/icons/filter-add.png))。 分段作业按时间顺序排序，最新的分段作业首先出现。

![筛选器图标高亮显示。 选择此选项可查看指定受众的分段作业。](../assets/ui/monitor-audiences/filter-audience.png)

此时会显示过滤的受众仪表板。 **[!UICONTROL 受众]**&#x200B;卡显示上次评估作业和上次激活作业的状态、日期。

![受众卡。 显示有关上次评估作业和上次激活作业的信息。](../assets/ui/monitor-audiences/specified-audience-card.png)

仪表板本身会显示上次评估和激活作业的时间和状态、一个显示受众评估的用户档案计数的图表，以及已运行的分段作业的量度。 默认情况下，功能板显示过去24小时内的分段作业量度。

![筛选的受众仪表板。 将显示已为此受众运行的各种分段作业的信息。](../assets/ui/monitor-audiences/filter-audience.png)

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| ------ | ----------- |
| **[!UICONTROL 作业开始]** | 分段作业开始的日期和时间。 |
| **[!UICONTROL 类型]** | 指示分段作业的类型。 两个支持的作业类型是&#x200B;**激活**&#x200B;和&#x200B;**评估**&#x200B;作业。 |
| **[!UICONTROL 作业完成]** | 分段作业完成的日期和时间。 |
| **[!UICONTROL 处理时间]** | 完成分段作业所用的时间。 |
| **[!UICONTROL 作业状态]** | 分段作业的状态。 支持的值包括&#x200B;**[!UICONTROL Success]**、**[!UICONTROL In Progress]**&#x200B;和&#x200B;**[!UICONTROL Failed]**。 |
| **[!UICONTROL 轮廓计数]** | 分段作业正在评估的配置文件数。 每个用户应具有唯一的配置文件。 |
| **[!UICONTROL 标识已激活]** | 分段作业正在激活的身份数。 每个配置文件都可以有多个身份。 例如，用户档案可能包含电子邮件、电话号码和忠诚度编号作为身份。 |
| **[!UICONTROL 目标名称]** | 分段作业将激活到的目标的名称。 |

您可以通过选择过滤器图标（![过滤器图标）来进一步过滤到特定的分段作业并查看其详细信息。](/help/images/icons/filter.png))。 有两种不同类型的分段作业可以过滤：激活作业和评估作业。

### 激活作业详细信息 {#activation-job-details}

“激活作业数据流运行详细信息”页面显示有关运行的量度、数据流运行错误以及与分段作业相关的受众的信息。 激活作业用于激活指定目标的受众。

![激活作业仪表板。 将显示已为此受众运行的各种分段作业的信息。](../assets/ui/monitor-audiences/activation-job-dashboard.png)

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| ------ | ----------- |
| **[!UICONTROL 已接收配置文件]** | 激活流中接收的配置文件总数。 |
| **[!UICONTROL 身份已激活]** | 根据收到的配置文件，成功激活到目标的身份总数。 |
| **[!UICONTROL 身份已排除]** | 根据收到的用户档案，从激活到目标过程中排除的身份总数。 由于缺少属性或违反同意，可以排除这些身份。 |
| **[!UICONTROL 数据大小]** | 正在激活的数据流的大小。 |
| **[!UICONTROL 文件总数]** | 数据流中正在激活的文件总数。 |
| **[!UICONTROL 状态]** | 激活作业的当前状态。 |
| **[!UICONTROL 数据流运行开始]** | 激活作业开始的日期和时间。 |
| **[!UICONTROL 数据流运行结束]** | 激活作业结束的日期和时间。 |
| **[!UICONTROL 数据流运行ID]** | 当前激活作业的ID。 |
| **[!UICONTROL IMS组织ID]** | 激活作业所属的组织的ID。 |
| **[!UICONTROL 目标名称]** | 数据被激活到的目标的名称。 |

在受众部分下，您可以看到作为激活作业的一部分激活的受众列表。

![激活作业仪表板。 有关失败或排除的标识的信息会突出显示。](../assets/ui/monitor-audiences/activation-job-audiences.png)

对于“受众”部分，提供了以下量度：

| 量度 | 描述 |
| ------ | ----------- |
| **[!UICONTROL 名称]** | 已激活的受众的名称。 |
| **[!UICONTROL 身份已激活]** | 根据收到的配置文件，成功激活到目标的身份总数。 |
| **[!UICONTROL 身份已排除]** | 根据收到的用户档案，从激活到目标过程中排除的身份总数。 由于缺少属性或违反同意，可以排除这些身份。 |
| **[!UICONTROL 上次数据流运行状态]** | 为该受众运行的上一个激活作业的状态。 |
| **[!UICONTROL 上次数据流运行日期]** | 为该受众运行的上次激活作业的日期和时间。 |

此外，您还可以查看有关数据流运行错误的详细信息。 在数据流运行错误部分下，您可以查看失败的身份或排除的身份。 错误部分包括有关错误代码以及失败或排除的标识数量的详细信息。

![激活作业仪表板。 有关失败或排除的标识的信息会突出显示。](../assets/ui/monitor-audiences/activation-job-errors.png)

### 评估作业详细信息 {#evaluation-job-details}

“评估作业数据流运行详细信息”页面显示与分段作业相关的运行量度和受众信息。

![评估工作仪表板。 显示有关受众评估作业的信息。](../assets/ui/monitor-audiences/evaluation-job-details.png)

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| ------ | ----------- |
| **[!UICONTROL 配置文件总数]** | 正在评估的配置文件总数。 |
| **[!UICONTROL 状态]** | 评估作业的状态。 评估作业的可能状态包括&#x200B;**[!UICONTROL 成功]**&#x200B;和&#x200B;**[!UICONTROL 失败]**。 |
| **[!UICONTROL 作业开始]** | 评估作业开始的日期和时间。 |
| **[!UICONTROL 作业结束]** | 评估作业结束的日期和时间。 |
| **[!UICONTROL 作业类型]** | 分段作业的类型。 在这种情况下，它始终为&#x200B;**[!UICONTROL 区段评估]**&#x200B;作业。 |
| **[!UICONTROL 评估类型]** | 正在执行的评估类型。 这可以是&#x200B;**[!UICONTROL 批次]**&#x200B;或&#x200B;**[!UICONTROL 流式传输]**。 |
| **[!UICONTROL 作业ID]** | 评估作业的ID。 |
| **[!UICONTROL IMS组织ID]** | 评估作业所属的组织的ID。 |
| **[!UICONTROL 受众名称]** | 正在评估的受众的名称。 |
| **[!UICONTROL 受众ID]** | 正在评估的受众的ID。 |

在[!UICONTROL 受众]部分下，您可以看到作为评估作业的一部分进行评估的受众列表。 您可以使用搜索栏按名称筛选受众列表。

>[!IMPORTANT]
>
>此仪表板视图当前支持最多800个受众量度。

对于[!UICONTROL 受众]部分，以下量度可用：

| 量度 | 描述 |
| ------ | ----------- |
| **[!UICONTROL 名称]** | 正在评估的受众的名称。 |
| **[!UICONTROL 轮廓计数]** | 正在评估的配置文件数。 |

## 监控分段作业仪表板 {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="分段作业"
>abstract="分段作业视图包含有关所有受众的评估和导出作业的信息。"

要访问&#x200B;**[!UICONTROL 分段作业]**&#x200B;仪表板，请在[!UICONTROL 受众]仪表板中选择&#x200B;**[!UICONTROL 分段作业]**。 [!UICONTROL 监控]仪表板包含有关评估和导出作业的量度和信息。

>[!NOTE]
>
>每个受众监测仅支持&#x200B;**分段评估作业**。 分段导出作业仅支持组织级别的监控。

![将显示分段作业监视仪表板。 突出显示了在受众和分段作业之间切换的切换。](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

使用[!UICONTROL 分段作业]仪表板来了解是否准时执行配置文件评估和导出，并且没有任何例外，以便目标激活的下游服务可以具有最新评估的配置文件数据。

以下量度可用于分段作业：

| 量度 | 描述 |
| ------ | ----------- |
| **[!UICONTROL 分段作业]** | 指示分段作业的名称。 |
| **[!UICONTROL 类型]** | 指示分段作业的类型 — 导出或评估。 请注意，在这两种情况下，分段作业都会评估或导出属于组织的&#x200B;**所有**&#x200B;受众。 要了解有关导出作业的详细信息，请阅读[导出作业终结点](../../segmentation/api/export-jobs.md)的指南。 要了解有关评估作业的更多信息，请阅读有关[评估区段定义](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment)的教程。 |
| **[!UICONTROL 作业开始]** | 分段作业开始的日期和时间。 |
| **[!UICONTROL 作业结束]** | 分段作业完成的日期和时间。 |
| **[!UICONTROL 状态]** | 已完成作业的状态。 分段作业的可能状态包括成功或失败。 |
