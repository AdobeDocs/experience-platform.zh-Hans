---
description: 了解如何使用Adobe Experience Platform中的“作业计划”工具检查和解决计划的批处理作业问题。
solution: Experience Platform
title: 检查作业计划
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%

---


# 检查作业计划

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules]当前可作为受限版本使用，并且仅适用于以下Real-Time CDP作业：
>
> * 批量数据湖摄取
> * 批量配置文件摄取
> * 批次分段
> * 批量目标激活。

[!UICONTROL Job Schedules]提供了跨数据管道的所有已计划批处理作业的统一视图 — 从引入到目标激活。 检查执行状态，识别计划冲突，并在配置问题影响您的业务运营之前对其进行诊断。

使用作业计划调查失败、优化作业时间并了解数据湖摄取、配置文件处理、分段和目标激活之间的依赖关系。 有关解决常见配置问题的指导，请参阅有关[标识作业计划反模式](job-schedules-anti-patterns.md)的文档。

## 先决条件 {#prerequisites}

若要访问[!UICONTROL Job Schedules]，您需要&#x200B;**[!UICONTROL View Job Schedules]**&#x200B;和&#x200B;**[!UICONTROL View Profile Management]** [访问控制权限](/help/access-control/home.md#permissions)。

请与系统管理员联系以确保您拥有适当的权限。

## 快速入门 {#getting-started}

在使用[!UICONTROL Job Schedules]之前，您应该熟悉以下Experience Platform概念：

* **[批量摄取](../ingestion/batch-ingestion/overview.md)**：如何按计划时间间隔将数据加载到数据湖和配置文件存储中。
* **[分段](../segmentation/home.md)**：如何根据用户档案数据和区段定义评估和更新受众。
* **[实时客户个人资料](../profile/home.md)**：如何统一个人资料数据并提供用于分段和激活。
* **[目标](../destinations/home.md)**：将数据激活到下游系统和营销平台的位置和方式。

了解这些组件可帮助您解释作业执行模式并在问题发生时诊断问题。

## 了解“任务计划”界面 {#understanding-interface}

要访问[!UICONTROL Job Schedules]：

1. 在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Run and Operate]**。
2. 选择 **[!UICONTROL Job Schedules]**。

[!UICONTROL Job Schedules]页提供了所有已安排的批处理作业的概览。

![运行和操作左侧导航](assets/job-schedules/run-and-operate-left-nav.png)

### 摘要卡片 {#summary-cards}

在页面顶部，您可以看到摘要信息卡，这些信息卡可让您快速了解批处理作业。

![作业计划摘要卡片显示批处理作业的见解](assets/job-schedules/job-schedules-cards.png)

* **湖摄取运行**：已运行的数据湖摄取作业数。
* **配置文件引入运行**：已运行的配置文件引入作业数。
* **下一个分段**：何时运行下一个计划的分段作业。
* **下一个目标激活**：下一个计划的目标激活作业将运行的时间。

这些卡片可帮助您了解整个数据管道中的活动和即将到来的计划。 **湖摄取运行的值**&#x200B;和&#x200B;**配置文件摄取运行的值**&#x200B;根据所选的时间间隔（今天、昨天或过去7天）更改；下一次运行的卡片（**下一次分段**&#x200B;和&#x200B;**下一次目标激活**）不受时间选择器的影响。

### 时段选择器 {#time-period}

使用时间段选择器选择回溯多远才能查看计划的作业。

![作业计划中的时间段选择器UI的动画示例](assets/job-schedules/time-selector.gif)

* **今天**：查看为今天安排的作业（默认视图）。
* **昨天**：查看昨天运行的作业。
* **最近7天**：查看过去一周的作业。

### 批处理作业计划详细信息 {#job-schedules-details}

主视图显示批处理作业计划在一天中运行的时间。 您可以：

* **按数据集或实体查看作业**：左列显示数据集或处理作业的名称（例如，摄取数据集或分段作业）。
* **查看作业计时**：时间线显示每个作业计划运行的时间，视觉指示器标记计划时间。
* **筛选作业**：使用筛选图标缩小要包含在报告中的数据集范围。
* **了解作业类型**：底部的颜色编码图例可帮助您识别不同的作业类型：
   * **湖引入**（绿色）：数据引入数据湖
   * **配置文件摄取** （粉红色）：数据摄取到配置文件存储中
   * **分段**（浅蓝色）：受众评估作业
   * **配置文件导出** （蓝色）：配置文件数据的导出
   * **激活**（深灰色）：目标激活作业
   * **进行中** （分条）：当前正在运行或已排队的作业

此时间线视图可帮助您识别计划冲突、了解作业之间的依赖关系，并优化批处理计划。

## 识别配置问题 {#identifying-issues}

在查看作业计划时，您可能会注意到指示配置问题的模式。 常见问题包括：

* 作业已调度为过于接近，导致资源争用
* 在同一时间范围内运行的批过多
* 每日批处理作业过多的单个数据集
* 计划在分段运行前立即进行的引入作业

这些模式可能会导致作业失败、数据处理不完整和系统性能不佳。 要了解如何识别和解决这些问题，请参阅有关[识别作业计划反模式](job-schedules-anti-patterns.md)的文档。

当需要调查特定数据集或作业运行时，可以深入查看详细视图，以查看执行历史记录、错误消息、性能度量和依赖关系。 有关查看此详细数据的信息，请参阅有关[查看作业详细信息](job-schedules-details.md)的文档。


## 后续步骤 {#next-steps}

了解工作计划后，您可能需要浏览以下相关主题：

* [查看作业详细信息](job-schedules-details.md)：了解如何深入了解各个数据集和作业运行情况以便进行详细调查。
* [识别作业计划反模式](job-schedules-anti-patterns.md)：了解如何发现并解决影响管道性能的常见配置问题。
* [批量摄取](../ingestion/batch-ingestion/overview.md)：了解如何使用批处理将数据摄取到Experience Platform。
* [分段](../segmentation/home.md)：了解如何按计划时间间隔评估和更新受众。
* [监视目标的数据流](../dataflows/ui/monitor-destinations.md)：了解如何监视目标激活数据流。
* [计划受众导出](../destinations/ui/activate-batch-profile-destinations.md)：了解如何配置计划的批处理目标激活。
