---
title: 查询时间表
description: 了解如何自动运行计划的查询、删除或禁用查询计划，以及通过Adobe Experience Platform UI利用可用的计划选项。
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 0%

---

# 查询计划

您可以通过创建查询计划来自动运行查询。 计划的查询以自定义节奏运行，以根据频率、日期和时间管理您的数据。 如果需要，您还可以为结果选择输出数据集。 可以从“查询编辑器”安排已另存为模板的查询。

>[!IMPORTANT]
>
>您只能将计划添加到已创建和保存的查询中。

任何计划查询都会添加到的列表 [!UICONTROL 计划的查询] 选项卡。 在该工作区中，您可以通过UI监控所有已计划查询作业的状态。 在 [!UICONTROL 计划的查询] 选项卡，您可以找到有关查询运行的重要信息并订阅警报。 可用信息包括运行失败时的状态、计划详细信息和错误消息/代码。 请参阅 [监视计划查询文档](./monitor-queries.md) 以了解更多信息。

此工作流涵盖查询服务UI中的计划过程。 要了解如何使用API添加计划，请参阅 [计划查询端点指南](../api/scheduled-queries.md).

## 创建查询计划 {#create-schedule}

要计划查询，请从以下任一位置选择查询模板 [!UICONTROL 模板] 选项卡或 [!UICONTROL 模板] 列 [!UICONTROL 计划的查询] 选项卡。 选择模板名称可将您导航到查询编辑器。

如果从“查询编辑器”访问已保存的查询，则可以为查询创建计划，或从详细信息面板查看查询计划。

>[!TIP]
>
>选择 **[!UICONTROL 查看计划]** 导航到计划工作区，并快速查看任何计划的查询运行。

![具有的查询编辑器 [!UICONTROL 查看计划] 和 [!UICONTROL 添加计划] 突出显示。](../images/ui/query-schedules/view-add-schedule.png)

选择 **[!UICONTROL 添加计划]** 导航到 [“调度详细资料”页](#schedule-details).

或者，选择 **[!UICONTROL 时间表]** 选项卡。

![突出显示了“计划”选项卡的查询编辑器。](../images/ui/query-schedules/schedules-tab.png)

此时将显示计划工作区。 UI显示与模板关联的任何计划运行的列表。 选择 **[!UICONTROL 添加计划]** 创建计划。

![查询编辑器计划工作区中突出显示了添加计划。](../images/ui/query-schedules/add-schedule.png)

### 添加计划详细信息 {#schedule-details}

此时将显示“调度详细资料”页。 在此页上，可以编辑计划查询的各种详细信息。 详情包括 [计划查询的频度和工作日](#scheduled-query-frequency) 运行、开始和结束日期、要将结果导出到的数据集，以及 [查询状态警报](#alerts-for-query-status).

![突出显示“计划详细信息”面板。](../images/ui/query-schedules/schedule-details.png)

#### 计划的查询频率 {#scheduled-query-frequency}

您可以选择以下选项 **[!UICONTROL 频率]**：

- **[!UICONTROL 每小时]**：计划查询将在您选择的日期范围内每小时运行一次。
- **[!UICONTROL 每日]**：计划查询将每隔X天运行一次您选择的时间和日期时段。 请注意，所选时间位于 **UTC**&#x200B;而不是您当地的时区。
- **[!UICONTROL 每周]**：选定的查询将在选定的一周、时间和日期时段运行。 请注意，所选时间位于 **UTC**&#x200B;而不是您当地的时区。
- **[!UICONTROL 每月]**：选定的查询将在每个月的选定日期、时间和日期时段运行。 请注意，所选时间位于 **UTC**&#x200B;而不是您当地的时区。
- **[!UICONTROL 每年]**：选定的查询每年将在您选择的天、月、时间和日期时段运行。 请注意，所选时间位于 **UTC**&#x200B;而不是您当地的时区。

### 提供数据集详细信息 {#dataset-details}

通过将数据附加到现有数据集或创建新数据集并将数据附加到其中来管理查询结果。

选择 **[!UICONTROL 创建新数据集并将其附加到新数据集中]** 在首次执行查询时创建数据集。 后续执行继续将数据插入到该数据集中。 最后，提供数据集的名称和描述。

>[!IMPORTANT]
>
> 由于您使用的是现有数据集或创建新数据集，因此您需要 **非** 需要包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作为查询的一部分，因为数据集已设置。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作为您计划查询的一部分，将导致错误。

![计划详细信息面板，其中包含数据集详细信息和 [!UICONTROL 创建新数据集并将其附加到新数据集中] 选项突出显示。](../images/ui/query-schedules/dataset-details-create-and-append.png)

或者，选择 **[!UICONTROL 附加到现有数据集]** 后跟数据集图标(![数据集图标。](../images/ui/query-schedules/dataset-icon.png))。

![计划详细信息面板，其中突出显示数据集详细信息并将其附加到现有数据集。](../images/ui/query-schedules/dataset-details-existing.png)

此 **[!UICONTROL 选择输出数据集]** 出现对话框。

接下来，浏览现有数据集或使用搜索字段筛选选项。 选择要使用的数据集的行。 数据集详细信息将显示在右侧的面板中。 选择 **[!UICONTROL 完成]** 确认您的选择。

![选择输出数据集对话框会突出显示搜索字段、数据集行和完成。](../images/ui/query-schedules/select-output-dataset-dialog.png)

### 如果查询连续失败，则将其隔离 {#quarantine}

创建计划时，您可以在隔离功能中注册查询，以保护系统资源并防止出现潜在的中断情况。 隔离功能会自动识别并隔离反复失败(通过将查询置于 [!UICONTROL 已隔离] 省/州。 通过在连续失败10次后隔离查询，您可以在允许进一步执行之前干预、查看和纠正问题。 这有助于保持您的操作效率和数据完整性。

![查询计划工作区 [!UICONTROL 查询隔离] 高亮显示并选中“是”。](../images/ui/query-schedules/quarantine-enroll.png)

在查询注册隔离功能后，您可以订阅此查询状态更改警报。 如果计划查询未注册隔离，它不会显示为上的选项 [警报对话框](./monitor-queries.md#alert-subscription).

您还可以通过的内联操作，将计划查询注册到隔离功能 [!UICONTROL 计划的查询] 选项卡。 请参阅 [监控查询文档](./monitor-queries.md#alert-subscription) 以了解更多详细信息。

### 为计划的查询状态设置警报 {#alerts-for-query-status}

您还可以订阅查询警报，作为计划查询设置的一部分。 这意味着您会在查询状态发生更改时收到通知。 可以以弹出通知或电子邮件的形式接收警报。 可用的查询状态警报选项包括“开始”、“成功”和“失败”。 选中该复选框可订阅针对该计划查询状态的警报。

![计划详细信息面板，其中突出显示了警报选项。](../images/ui/query-editor/alerts.png)

有关Adobe Experience Platform中警报的概述，包括定义警报规则的结构，请参阅 [警报概述](../../observability/alerts/overview.md). 有关在Adobe Experience Platform UI中管理警报和警报规则的指导，请参阅 [警报UI指南](../../observability/alerts/ui.md).

### 为计划的参数化查询设置参数 {#set-parameters}

>[!IMPORTANT]
>
>参数化查询UI功能当前在以下位置可用： **仅限限量发布** 并非所有客户均适用。 如果您无权访问参数化查询，请继续访问 [删除或禁用计划](#delete-schedule) 部分。

如果要为参数化查询创建计划查询，现在必须为这些查询运行设置参数值。

![计划创建工作流的“计划详细信息”部分，其中高亮显示查询参数部分。](../images/ui/query-schedules/scheduled-query-parameter.png)

确认计划详细信息后，选择 **[!UICONTROL 保存]** 创建计划。 您将返回到模板的“计划”选项卡。 此工作区显示新创建计划的详细信息，包括计划ID、计划本身以及计划的输出数据集。

## 查看计划的查询运行 {#scheduled-query-runs}

从模板的 [!UICONTROL 时间表] 选项卡，选择计划ID以导航到新计划查询的查询运行列表。

![突出显示新创建计划的计划工作区。](../images/ui/query-schedules/schedules-workspace.png)

或者，要查看查询模板的计划运行列表，请导航到 **[!UICONTROL 计划的查询]** 选项卡，并从可用的列表中选择模板名称。

![突出显示命名模板的“计划查询”选项卡。](../images/ui/query-schedules/view-scheduled-runs.png)

将显示该计划查询的查询运行列表。

![计划查询工作区的详细信息部分，其中包含为计划查询突出显示的查询运行列表。](../images/ui/query-schedules/list-of-scheduled-runs.png)

请参阅 [monitor scheduled queried指南](./monitor-queries.md#inline-actions) 有关如何通过UI监控所有查询作业状态的完整信息。

选择 **[!UICONTROL 查询运行Id]** 从列表中定位至“查询运行概览”。 欲知有关 [查询运行概述](./monitor-queries.md#query-run-overview)中，请参阅监视器计划查询文档。

要使用查询服务API监控计划查询，请参阅 [计划查询运行端点指南](../api/runs-scheduled-queries.md).

## 启用、禁用或删除计划 {#delete-schedule}

您可以从特定查询的计划工作区或以下位置启用、禁用或删除计划： [!UICONTROL 计划的查询] 列出所有计划查询的工作区。

要访问 [!UICONTROL 时间表] 选项卡中，您必须从以下任一位置选择查询模板的名称： [!UICONTROL 模板] 选项卡或 [!UICONTROL 计划的查询] 选项卡。 这将导航到该查询的查询编辑器。 从查询编辑器中，选择 **[!UICONTROL 时间表]** 以访问时间表工作区。

从可用计划的行中选择一个计划以填充详细信息面板。 使用切换可禁用（或启用）计划查询。

### 删除禁用的查询

>[!IMPORTANT]
>
>您必须先禁用计划，然后才能删除查询的计划。

![突出显示详细信息面板的模板计划列表。](../images/ui/query-schedules/schedule-details-panel.png)

将显示确认对话框。 选择 **[!UICONTROL 禁用]** 以确认操作。

![禁用计划确认对话框。](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

选择 **[!UICONTROL 删除计划]** 删除已禁用的计划。

![计划工作区中突出显示了删除计划。](../images/ui/query-schedules/delete-schedule.png)

或者， [!UICONTROL 计划的查询] 选项卡提供每个计划查询的内联操作集合。 可用的内联操作包括 [!UICONTROL 禁用计划] 或 [!UICONTROL 启用计划]， [!UICONTROL 删除计划]、和 [!UICONTROL 订阅] 用于计划查询的警报。 有关如何通过“计划查询”选项卡删除或禁用计划查询的完整说明，请参阅 [monitor scheduled queried指南](./monitor-queries.md#inline-actions).
