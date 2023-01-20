---
title: 查询计划
description: 了解如何自动执行计划查询运行、删除或禁用查询计划，以及通过Adobe Experience Platform UI利用可用的计划选项。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# 查询计划

您可以通过创建查询计划来自动运行查询。 计划查询在自定义频率下运行，以根据频度、日期和时间管理数据。 您还可以根据需要为结果选择输出数据集。 可以从查询编辑器中计划已另存为模板的查询。

>[!IMPORTANT]
>
>以下是使用查询编辑器时计划查询的限制列表。 它们不适用于 [!DNL Query Service] API:<br/>您只能向已创建、保存和运行的查询添加计划。<br/>您 **无法** 向参数化查询添加计划。<br/>计划查询 **无法** 包含匿名块。

任何计划查询都将添加到 [!UICONTROL 计划查询] 选项卡。 在该工作区中，您可以通过UI监控所有计划查询作业的状态。 在 [!UICONTROL 计划查询] 选项卡，您可以找到有关查询运行和订阅警报的重要信息。 可用信息包括状态、计划详细信息以及运行失败时的错误消息/代码。 请参阅 [监视计划查询文档](./monitor-queries.md) 以了解更多信息。

## 创建查询计划 {#create-schedule}

要向查询添加计划，请从 [!UICONTROL 模板] 选项卡 [!UICONTROL 计划查询] 选项卡，导航到查询编辑器。

要了解如何使用API添加计划，请阅读 [计划查询终结点指南](../api/scheduled-queries.md).

从查询编辑器访问保存的查询时， [!UICONTROL 计划] 选项卡。 选择 **[!UICONTROL 计划]**.

![突出显示了“计划”选项卡的查询编辑器。](../images/ui/query-schedules/schedules-tab.png)

此时将显示计划工作区。 选择 **[!UICONTROL 添加计划]** 创建计划。

![查询编辑器计划工作区中突出显示了添加计划。](../images/ui/query-schedules/add-schedule.png)

此时将显示计划详细信息页面。 在此页面上，您可以选择计划查询的频率、开始和结束日期、计划查询将在一周中运行的日期，以及要将查询导出到的数据集。

![“计划详细信息”面板突出显示。](../images/ui/query-schedules/schedule-details.png)

您可以为 **[!UICONTROL 频率]**:

- **[!UICONTROL 每小时]**:在您选择的日期期间，计划查询将每小时运行一次。
- **[!UICONTROL 每日]**:计划查询将在您选择的时间和日期期间每X天运行一次。 请注意，选择的时间在 **UTC**，而不是您的本地时区。
- **[!UICONTROL 每周]**:所选查询将在您选择的周、时间和日期期间的天数运行。 请注意，选择的时间在 **UTC**，而不是您的本地时区。
- **[!UICONTROL 每月]**:选定的查询将每月在您选择的日期、时间和日期期间运行。 请注意，选择的时间在 **UTC**，而不是您的本地时区。
- **[!UICONTROL 每年]**:选定的查询将每年在您选择的日期、月、时间和日期期间运行。 请注意，选择的时间在 **UTC**，而不是您的本地时区。

对于输出数据集，您可以选择使用现有数据集或创建新数据集。

>[!IMPORTANT]
>
> 由于您使用的是现有数据集或创建了新数据集，因此需要 **not** 需要包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作为查询的一部分，因为数据集已经设置。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作为计划查询的一部分，将导致错误。

确认所有这些详细信息后，选择 **[!UICONTROL 保存]** 创建计划。 您将返回到计划工作区，该工作区显示新创建计划的详细信息，包括计划ID、计划本身和计划的输出数据集。 您可以使用计划ID查找有关计划查询本身运行的更多信息。 要了解更多信息，请阅读 [计划查询运行端点指南](../api/runs-scheduled-queries.md).

![计划工作区中突出显示了新创建的计划。](../images/ui/query-schedules/schedules-workspace.png)

## 删除或禁用计划 {#delete-schedule}

您可以从计划工作区中删除或禁用计划。 您必须从 [!UICONTROL 模板] 选项卡 [!UICONTROL 计划查询] 选项卡，导航到查询编辑器并选择 **[!UICONTROL 计划]** 以访问“计划”工作区。

从可用计划的行中选择计划。 您可以使用切换开关来禁用或启用计划查询。

>[!IMPORTANT]
>
>在删除查询计划之前，必须先禁用该计划。

选择 **[!UICONTROL 删除计划]** 删除禁用的计划。

![“禁用计划”和“删除计划”会突出显示计划工作区。](../images/ui/query-schedules/delete-schedule.png)


