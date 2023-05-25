---
title: 查询时间表
description: 了解如何通过Adobe Experience Platform UI自动运行计划的查询、删除或禁用查询计划以及利用可用的计划选项。
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# 查询计划

您可以通过创建查询计划来自动运行查询。 计划的查询在自定义节奏上运行，以根据频率、日期和时间管理您的数据。 如果需要，您还可以为结果选择输出数据集。 可以从“查询编辑器”安排已另存为模板的查询。

>[!IMPORTANT]
>
>以下是使用查询编辑器时计划查询的限制列表。 它们不适用于 [!DNL Query Service] API：<br/>您只能向已创建、保存和运行的查询添加计划。<br/>您 **无法** 将计划添加到参数化查询。<br/>计划的查询 **无法** 包含匿名块。

任何计划的查询都会添加到的列表 [!UICONTROL 计划的查询] 选项卡。 在该工作区中，您可以通过UI监控所有已计划查询作业的状态。 在 [!UICONTROL 计划的查询] 选项卡，您可以找到有关查询运行的重要信息并订阅警报。 可用信息包括运行失败时的状态、计划详细信息和错误消息/代码。 请参阅 [监视计划查询文档](./monitor-queries.md) 了解更多信息。

## 创建查询计划 {#create-schedule}

要向查询添加计划，请从以下任一位置选择查询模板 [!UICONTROL 模板] 选项卡或 [!UICONTROL 计划的查询] 选项卡，导航到查询编辑器。

要了解如何使用API添加计划，请阅读 [计划查询端点指南](../api/scheduled-queries.md).

当从查询编辑器访问保存的查询时， [!UICONTROL 时间表] 选项卡显示在查询名称下方。 选择 **[!UICONTROL 时间表]**.

![突出显示“计划”选项卡的查询编辑器。](../images/ui/query-schedules/schedules-tab.png)

此时将显示时间表工作区。 选择 **[!UICONTROL 添加计划]** 创建计划。

![查询编辑器计划工作区中突出显示了添加计划。](../images/ui/query-schedules/add-schedule.png)

此时将显示“调度详细资料”页。 在此页面上，您可以选择计划查询的频率、开始和结束日期、运行计划查询的星期几以及要将查询导出到哪个数据集。

![突出显示“计划详细信息”面板。](../images/ui/query-schedules/schedule-details.png)

您可以选择以下选项 **[!UICONTROL 频率]**：

- **[!UICONTROL 每小时]**：计划查询将在您选择的日期时段内每小时运行一次。
- **[!UICONTROL 每日]**：计划查询将每隔X天运行一次您选择的时间和日期时段。 请注意，所选时间位于 **UTC**&#x200B;而不是您的本地时区。
- **[!UICONTROL 每周]**：所选查询将在所选的一周、时间和日期时段中运行。 请注意，所选时间位于 **UTC**&#x200B;而不是您的本地时区。
- **[!UICONTROL 每月]**：选定的查询将在每月选定的日期、时间和日期时段运行。 请注意，所选时间位于 **UTC**&#x200B;而不是您的本地时区。
- **[!UICONTROL 每年]**：选定的查询每年将在选定的日期、月、时间和日期时段运行。 请注意，所选时间位于 **UTC**&#x200B;而不是您的本地时区。

对于输出数据集，您可以选择使用现有数据集或创建新数据集。

>[!IMPORTANT]
>
> 由于您使用的是现有数据集或创建新数据集，因此您需要 **非** 需要包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作为查询的一部分，因为数据集已设置。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作为计划查询的一部分，将导致错误。

确认所有这些详细信息后，选择 **[!UICONTROL 保存]** 创建计划。 您将返回到显示新创建计划的详细信息的计划工作区，包括计划ID、计划本身和计划的输出数据集。 您可以使用计划ID查找有关运行计划查询本身的更多信息。 欲知更多信息，请阅读 [计划查询运行端点指南](../api/runs-scheduled-queries.md).

![突出显示新创建计划的计划工作区。](../images/ui/query-schedules/schedules-workspace.png)

## 删除或禁用计划 {#delete-schedule}

您可以从计划工作区中删除或禁用计划。 您必须从以下任一位置选择查询模板 [!UICONTROL 模板] 选项卡或 [!UICONTROL 计划的查询] 选项卡，导航到查询编辑器并选择 **[!UICONTROL 计划]** 以访问时间表工作区。

从可用计划行中选择一个计划。 您可以使用切换开关禁用或启用计划查询。

>[!IMPORTANT]
>
>您必须先禁用计划，然后才能删除查询的计划。

选择 **[!UICONTROL 删除计划]** 删除已禁用的计划。

![突出显示具有“禁用计划”和“删除”计划的计划工作区。](../images/ui/query-schedules/delete-schedule.png)
