---
description: 了解如何在“作业计划”中查看有关数据集和各个作业运行的详细信息。
solution: Experience Platform
title: 查看作业计划详细信息
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 1%

---


# 查看作业计划详细信息

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules]当前可作为受限版本使用，并且仅适用于以下Real-Time CDP作业：
>
> * 批量数据湖摄取
> * 批量配置文件摄取
> * 批次分段
> * 批量目标激活。

在排除作业故障或调查性能问题时，您需要有关特定数据集及其作业运行的详细信息。 [作业计划](job-schedules.md)界面允许您从时间线视图向下钻取到单个数据集和作业，以了解执行历史记录、时间和状态。

使用此详细视图可以：

* 调查特定作业失败或所用时间长于预期的原因
* 查看一段时间内数据集的执行历史记录
* 了解批处理作业的时间和持续时间模式
* 识别导致管道问题的特定批次
* 收集通过Adobe支持进行故障排除所需的信息

## 先决条件 {#prerequisites}

在查看作业详细信息之前，您应：

* 具有[!UICONTROL Job Schedules]和&#x200B;**[!UICONTROL View Job Schedules]**&#x200B;的&#x200B;**[!UICONTROL View Profile Management]**&#x200B;访问控制权限[的访问权限](/help/access-control/home.md#permissions)。
* 熟悉[作业计划界面](job-schedules.md#understanding-interface)和时间线视图。
* 了解不同的[作业类型](job-schedules.md#job-schedules-details)（湖摄取、配置文件摄取、分段、激活）。

## 了解详细信息层次结构 {#details-hierarchy}

作业计划提供三个详细级别，使您能够从广泛的模式移动到特定的问题：

| 视图级别 | 它显示的内容 | 何时使用 |
|------------|---------------|----------------|
| **时间线视图** | 选定时间段内的所有数据集及其计划作业 | 识别模式，发现[反模式](job-schedules-anti-patterns.md)，并获取整个管道的概述 |
| **数据集详细信息** | 单个数据集的汇总量度和执行历史记录 | 跟踪一个数据集的总体性能，了解数据量，并审查作业频率 |
| **作业运行详细信息** | 单个作业运行的特定执行信息 | 调查特定作业失败的原因，检查确切时间，并验证已处理的记录 |

**导航流**：从时间线视图开始以识别问题→选择数据集以查看其详细信息→选择特定作业运行以调查详细信息。

### 了解时间线视图 {#timeline-visualization}

时间线视图使用水平和垂直布局来帮助您了解任务计划和关键处理时间：

* **水平轴（时间进度）**：数据集及其作业运行在时间轴上从左到右显示，显示作业在选定时段（今天、昨天或过去7天）内的执行时间。 每个彩色条表示作业运行，根据其开始和结束时间水平放置。

* **垂直轴（计划的开始时间）**：关键计划的开始时间显示为横跨所有数据集的垂直线，以便轻松查看上游作业与下游处理之间的时间关系：
   * **蓝色垂直线**：表示计划何时开始分段
   * **黑色垂直线**：表示目标激活计划何时开始

利用此布局，可快速识别数据管道作业与下游处理之间的时间关系。 理想情况下，上游作业（如数据湖和配置文件摄取）应在这些垂直标记的左侧完成，以确保数据在分段和激活开始之前准备就绪。 延伸超过这些标记的任务指示了潜在的计时问题，其中下游流程可能在数据完全准备之前启动。

### 我应该使用哪个视图？ {#which-view}

| 我需要…… | 使用此视图 |
|--------------|---------------|
| 一次查看所有我的启用配置文件的数据集及其计划 | [时间线视图](job-schedules.md) |
| 识别计划冲突或反模式 | [时间线视图](job-schedules.md) |
| 跟踪一个数据集的整体性能 | [数据集详细信息](#view-dataset-details) |
| 查看数据集已处理的记录总数 | [数据集详细信息](#view-dataset-details) |
| 比较一个数据集在一段时间内的作业性能 | [数据集详细信息](#view-dataset-details) |
| 调查特定作业失败的原因 | [作业运行详细信息](#view-job-details) |
| 检查特定作业执行的确切时间 | [作业运行详细信息](#view-job-details) |
| 验证在单个运行中处理的记录 | [作业运行详细信息](#view-job-details) |
| 访问详细的错误消息 | [作业运行详细信息](#view-job-details) →选择数据流运行ID |

## 查看数据集详细信息 {#view-dataset-details}

要查看特定数据集的详细信息，请执行以下操作：

1. 在&#x200B;**[!UICONTROL Job Schedules]**&#x200B;时间线视图中，找到要调查的数据集。
2. 从左列中选择数据集名称。

数据集详细信息视图将在右侧面板中打开，显示与此数据集关联的所有作业的信息。

![数据集详细信息面板显示选定数据集的聚合湖和配置文件摄取量度。](assets/job-schedules/view-dataset-details.png)

数据集详细信息面板显示按作业类型组织的数据集名称、ID和作业特定的量度。 在面板顶部，数据集ID显示为可单击的链接。 选择此ID可导航到完整数据集详细信息页面。

每个数据集详细信息面板包括以下量度：

### 湖摄取量度 {#lake-ingestion-metrics}

对于包含数据湖摄取作业的数据集，面板会显示以下量度：

| 量度 | 描述 | 用于 |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | 已为此数据集完成的数据湖摄取作业总数 | 活动跟踪 |
| **[!UICONTROL Runs in progress]** | 当前正在运行多少个湖引入作业 | 瓶颈检测 |
| **[!UICONTROL Total records added]** | 所有作业运行时添加到数据湖的新记录的累积数 | 卷监测 |
| **[!UICONTROL Total ingestion time]** | 所有数据湖摄取作业的总持续时间 | 处理时间评估 |
| **[!UICONTROL Total records updated]** | 摄取期间更新的现有记录的累积数 | 刷新模式分析 |
| **[!UICONTROL Avg. ingestion speed (records/second)]** | 数据湖摄取作业的平均吞吐率 | 性能比较 |

### 配置文件摄取量度 {#profile-ingestion-metrics}

对于包含配置文件摄取作业的数据集，该面板会显示以下量度：

| 量度 | 描述 | 用于 |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | 已为此数据集完成的配置文件引入作业的总数 | 活动跟踪 |
| **[!UICONTROL Runs in progress]** | 当前正在运行多少个配置文件引入作业 | 延迟检测 |
| **[!UICONTROL Total profiles created]** | 所有作业运行中从此数据集创建的新配置文件的累计数量 | 配置文件增长监控 |
| **[!UICONTROL Total profile ingestion time]** | 所有配置文件摄取作业的总持续时间 | 时间问题识别 |
| **[!UICONTROL Total profiles updated]** | 已使用此数据集中的数据更新的现有用户档案的累积数 | 更新频率跟踪 |
| **[!UICONTROL Avg. profile ingestion speed (profiles/second)]** | 配置文件摄取作业的平均吞吐率 | 性能监控 |

>[!NOTE]
>
> 这些量度显示此数据集的所有作业运行的累计总数。 要查看特定运行的详细信息，请直接从时间线中选择作业。

## 在时间轴中筛选数据集 {#filter-datasets}

当有许多包含计划作业的数据集时，您可能希望将重点放在特定数据集上，而不是一次查看所有数据集。 数据集过滤器允许您选择要在时间轴视图中显示的数据集。

![数据集筛选器面板，允许您选择要在时间线视图中显示的数据集。](assets/job-schedules/view-datasets.gif)

要筛选时间轴中显示的数据集，请执行以下操作：

1. 在时间轴视图的左上角查找数据集计数器（例如，“2个数据集”）。
2. 选择数据集计数器旁边的过滤器图标。
3. 此时将打开一个数据集选择面板，其中显示所有具有计划作业且支持配置文件的可用数据集。
4. 选择或取消选择要在时间轴视图中显示或隐藏的数据集。
5. 时间轴会立即更新以仅显示选定的数据集。

使用过滤可以：

* **专注于特定数据源**：对特定数据管道进行故障排除时，请进行筛选以仅显示相关数据集。
* **降低视觉混乱**：如果您有许多数据集，那么过滤功能可帮助您更清楚地查看数据子集的模式。
* **比较相关数据集**：仅选择与了解其计划关系相关的数据集。
* **调查反模式**：当您发现潜在的[配置问题](job-schedules-anti-patterns.md)时，请筛选到受影响的数据集以更仔细地检查它们。

该过滤器在您的会话期间持续存在，因此您可以在时间段（今天、昨天、过去7天）之间导航，同时保持您的数据集选择。

## 查看单个作业运行详细信息 {#view-job-details}

当需要调查特定作业运行时，请从时间线中选择该作业以查看该特定运行的详细执行信息。

### 访问作业运行详细信息 {#access-job-details}

要查看特定作业运行的详细信息，请执行以下操作：

1. 在[!UICONTROL Job Schedules]时间线视图中，找到要调查的特定作业运行。
2. 选择时间线上的作业指示器（表示作业的彩色条）。

此时将打开&#x200B;**[!UICONTROL Dataflow run details]**&#x200B;面板，显示有关该特定作业执行的信息。

![数据流运行详细信息面板，显示特定作业运行的执行信息。](assets/job-schedules/job-details.png)

### 数据流运行详细信息 {#dataflow-run-details}

数据流运行详细信息面板按作业类型显示有关特定作业运行的信息。 对于摄取作业，您将看到湖摄取和配置文件摄取阶段的详细信息。

#### 湖摄取作业详细信息 {#lake-ingestion-job-details}

| 字段 | 描述 |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | 此特定湖摄取作业运行的唯一标识符。 选择ID可查看完整的数据流监视详细信息。 |
| **[!UICONTROL Run status]** | 作业的结果（成功、失败、进行中、已排队）。 绿色指示器显示成功完成。 |
| **[!UICONTROL Started at]** | 湖引入作业开始执行的日期和时间。 |
| **[!UICONTROL Completed at]** | 湖摄取作业完成执行的日期和时间。 |
| **[!UICONTROL Records added]** | 在此作业运行期间添加到数据湖的新记录数。 |
| **[!UICONTROL Records updated]** | 在此作业运行期间在数据湖中更新的现有记录数。 |

#### 配置文件摄取作业详细信息 {#profile-ingestion-job-details}

| 字段 | 描述 |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | 此特定配置文件摄取作业运行的唯一标识符。 选择ID可查看完整的数据流监视详细信息。 |
| **[!UICONTROL Run status]** | 作业的结果（成功、失败、进行中、已排队）。 绿色指示器显示成功完成。 |
| **[!UICONTROL Started at]** | 配置文件引入作业开始执行的日期和时间。 |
| **[!UICONTROL Completed at]** | 配置文件摄取作业完成执行的日期和时间。 |
| **[!UICONTROL Records added]** | 在此作业运行期间创建的新配置文件数。 |
| **[!UICONTROL Records updated]** | 在此作业运行期间更新的现有配置文件的数量。 |

### 了解作业执行流程 {#job-execution-flow}

查看特定作业运行时，您可以查看湖摄取和配置文件摄取之间的关系：

* **湖摄取首先运行**：数据已加载到数据湖并进行验证。
* **配置文件摄取遵循**：湖摄取完成后，符合条件的记录将被处理到配置文件存储中。
* **时间很重要**：请注意湖摄取完成时和配置文件摄取开始时之间的时间差。 此处的差距可能会影响下游流程，如分段。

**将作业运行详细信息用于**：

* 验证特定作业是否成功完成
* 计算作业运行的实际持续时间（完成时间减去开始时间）
* 了解在特定运行中处理了多少记录
* 比较不同作业运行的性能
* 访问详细的数据流监控以进行故障排除
* 确定湖和配置文件摄取阶段之间的时间问题

## 作业详细信息疑难解答 {#troubleshooting}

使用作业详细信息调查问题并确定后续步骤：

**失败的作业**：选择数据流运行ID以在监视仪表板中查看错误详细信息。 检查[数据集详细信息](#view-dataset-details)以了解周期性模式，查看[时间线](job-schedules.md)以了解资源争用，并在您的配置中识别[反模式](job-schedules-anti-patterns.md)。

**缓慢作业**：将持续时间与[数据集量度](#view-dataset-details)中的历史平均值进行比较。 常见原因包括[计划重叠](job-schedules-anti-patterns.md#schedule-overlap-pattern)、[密集批次栈叠](job-schedules-anti-patterns.md#scheduled-density)或数据量增加。

**记录不匹配**：将湖摄取记录与作业运行详细信息中的配置文件摄取记录进行比较。 由于身份要求和数据质量规则，配置文件摄取通常显示的记录较少。

有关详细的数据流状态信息，请参阅[监视数据湖摄取](../dataflows/ui/monitor-sources.md)、[监视个人资料的数据流](../dataflows/ui/monitor-profiles.md)、[监视受众的数据流](../dataflows/ui/monitor-audiences.md)和[监视目标的数据流](../dataflows/ui/monitor-destinations.md)。

## 后续步骤 {#next-steps}

了解如何查看作业详细信息后：

* 查看[作业计划概述](job-schedules.md)以了解时间线视图和界面。
* 了解[反模式](job-schedules-anti-patterns.md)以防止常见配置问题。
* 了解[批量摄取](../ingestion/batch-ingestion/overview.md)以优化数据加载计划。
* 浏览[监视目标数据流](../dataflows/ui/monitor-destinations.md)以了解端到端管道可见性。
