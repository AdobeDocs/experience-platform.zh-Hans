---
title: 监视计划查询
description: 了解如何通过查询服务UI监控查询。
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 1b4554e204663d40c3a18da792614305abb7d296
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---

# 监视计划查询

Adobe Experience Platform通过UI提高了所有查询作业状态的可见性。 起始日期 [!UICONTROL 计划的查询] 选项卡您现在可以找到有关查询运行的重要信息，包括状态、计划详细信息以及失败时的错误消息/代码。 您还可以通过UI为任何此类查询订阅基于其状态的查询警报，方法是使用 [!UICONTROL 计划的查询] 选项卡。

## [!UICONTROL 计划的查询]

此 [!UICONTROL 计划的查询] 选项卡提供了所有计划CTA和ITAS查询的概述。 可以找到所有计划查询的运行详细信息，以及任何失败查询的错误代码和消息。

要导航到 [!UICONTROL 计划的查询] 选项卡，选择 **[!UICONTROL 查询]** 导航栏中，后面是 **[!UICONTROL 计划的查询]**

![“查询”工作区中的“计划查询”选项卡。](../images/ui/monitor-queries/scheduled-queries.png)

下表描述了每个可用的列。

>[!NOTE]
>
>警报订阅图标包含在无标题列的每一行中。 请参阅 [警报订阅](#alert-subscription) 部分以了解更多信息。

| 栏目 | 描述 |
|---|---|
| **[!UICONTROL 名称]** | 名称字段是模板名称或SQL查询的前几个字符。 使用查询编辑器通过UI创建的任何查询都会在开始时命名。 如果查询是通过API创建的，则其名称将成为用于创建查询的初始SQL的片段。 从中选择任意项目 [!UICONTROL 名称] 列，以查看与查询关联的所有运行的列表。 欲了解更多信息，请参见 [查询运行计划详细信息](#query-runs) 部分。 |
| **[!UICONTROL 模板]** | 查询的模板名称。 选择模板名称以导航到“查询编辑器”。 为方便起见，查询编辑器中会显示查询模板。 如果没有模板名称，该行将标有连字符，并且无法重定向到查询编辑器以查看查询。 |
| **[!UICONTROL SQL]** | SQL查询的片段。 |
| **[!UICONTROL 运行频率]** | 这是您的查询设置为运行的节奏。 可用的值包括 `Run once` 和 `Scheduled`. 可以根据查询的运行频率对其进行筛选。 |
| **[!UICONTROL 创建者]** | 创建查询的用户的名称。 |
| **[!UICONTROL 已创建]** | 创建查询时的时间戳（UTC格式）。 |
| **[!UICONTROL 上次运行时间戳]** | 运行查询时的最新时间戳。 此列突出显示查询是否已根据其当前计划执行。 |
| **[!UICONTROL 上次运行状态]** | 最近查询执行的状态。 状态值包括： `Success`， `Failed`， `In progress`、和 `No runs`. |

>[!TIP]
>
>如果导航到查询编辑器，则可以选择 **[!UICONTROL 查询]** 以返回 [!UICONTROL 模板] 选项卡。

### 自定义计划查询的表设置

您可以调整上的列 [!UICONTROL 计划的查询] 轻松满足您的需求。 选择设置图标(![设置图标。](../images/ui/monitor-queries/settings-icon.png))以打开 [!UICONTROL 自定义表] “设置”对话框和编辑可用列。

![自定义表格设置图标。](../images/ui/monitor-queries/customze-table-settings-icon.png)

切换相关的复选框以删除或添加表列。 接下来，选择 **[!UICONTROL 应用]** 以确认您的选择。

>[!NOTE]
>
>通过UI创建的任何查询都将在创建过程中成为命名模板。 模板名称显示在模板列中。 如果查询是通过API创建的，则模板列为空。

![自定义表设置对话框。](../images/ui/monitor-queries/customize-table-dialog.png)

### 订阅警报 {#alert-subscription}

您可以从以下位置订阅警报： [!UICONTROL 计划的查询] 选项卡。 选择警报通知图标(![警报图标。](../images/ui/monitor-queries/alerts-icon.png))以打开 [!UICONTROL 警报] 对话框。 此 [!UICONTROL 警报] 对话框同时订阅UI通知和电子邮件警报。 警报基于查询的状态。 有三个可用选项： `start`， `success`、和 `failure`. 选中相应的一个或多个框并选择 **[!UICONTROL 保存]** 订购。

![警报订阅对话框。](../images/ui/monitor-queries/alert-subscription-dialog.png)

请参阅 [警报订阅API文档](../api/alert-subscriptions.md) 了解更多信息。

### 筛选查询 {#filter}

您可以根据运行频率筛选查询。 从 [!UICONTROL 计划的查询] 选项卡，选择过滤器图标(![过滤器图标](../images/ui/monitor-queries/filter-icon.png))以打开过滤器侧栏。

![突出显示过滤器图标的计划查询选项卡。](../images/ui/monitor-queries/filter-queries.png)

选择 **[!UICONTROL 已计划]** 或 **[!UICONTROL 运行一次]** 运行频率筛选器复选框以筛选查询列表。

>[!NOTE]
>
>任何已执行但未计划的查询均符合 [!UICONTROL 运行一次].

![突出显示过滤器侧栏的计划查询选项卡。](../images/ui/monitor-queries/filter-sidebar.png)

启用筛选条件后，选择 **[!UICONTROL 隐藏筛选器]** 以关闭过滤器面板。

## 查询运行计划详细信息 {#query-runs}

选择查询名称以定位至“计划详细资料”页。 此视图提供在该计划查询中执行的所有运行的列表。 提供的信息包括开始和结束时间、状态以及所使用的数据集。

![“调度详细资料”页。](../images/ui/monitor-queries/schedule-details.png)

此信息以五列表格形式提供。 每一行表示查询执行。

| 列名称 | 描述 |
|---|---|
| **[!UICONTROL 查询运行Id]** | 每日执行的查询运行ID。 选择 **[!UICONTROL 查询运行Id]** 导航到 [!UICONTROL 查询运行概述]. |
| **[!UICONTROL 查询运行开始]** | 执行查询的时间戳。 这是UTC格式。 |
| **[!UICONTROL 查询运行完成]** | 查询完成时的时间戳。 这是UTC格式。 |
| **[!UICONTROL 状态]** | 最近查询执行的状态。 三个状态值包括： `successful` `failed` 或 `in progress`. |
| **[!UICONTROL 数据集]** | 执行中涉及的数据集。 |

欲知正在计划的查询详情，请参阅 [!UICONTROL 属性] 面板。 此面板包括初始查询ID、客户端类型、模板名称、查询SQL和计划的节奏。

![突出显示属性面板的“计划详细信息”页面。](../images/ui/monitor-queries/properties-panel.png)

选择一个查询运行ID以定位至运行详细信息页并查看查询信息。

![突出显示运行ID的计划详细信息屏幕。](../images/ui/monitor-queries/navigate-to-run-details.png)

## 查询运行概述 {#query-run-overview}

此 [!UICONTROL 查询运行概述] 提供有关此计划查询的单独运行的信息，以及运行状态的更详细细分。 此页面还包括客户端信息以及可能导致查询失败的任何错误的详细信息。

![运行详细信息屏幕，其中高亮显示概述部分。](../images/ui/monitor-queries/query-run-details.png)

查询状态部分提供了查询失败时的错误代码和错误消息。

![运行详细信息屏幕，其中突出显示了错误部分。](../images/ui/monitor-queries/failed-query.png)

您可以从此视图将查询SQL复制到剪贴板。 选择SQL代码片段右上角的复制图标以复制查询。 此时会显示一条弹出消息，确认代码已被复制。

![突出显示SQL复制图标的运行详细信息屏幕。](../images/ui/monitor-queries/copy-sql.png)

### 使用匿名块运行查询的详细信息 {#anonymous-block-queries}

使用匿名块组成其SQL语句的查询被分隔到其各个子查询中。 这允许您分别检查每个查询块的运行详细信息。

>[!NOTE]
>
>使用DROP命令的匿名块的运行详细信息将 **非** 将作为单独的子查询报告。 CTAS查询、ITAS查询和用作匿名块子查询的COPY语句有单独的运行详细信息。 当前不支持DROP命令的运行详细信息。

匿名块通过使用 `$$` 在查询前添加前缀。 请参阅 [匿名阻止文档](../essential-concepts/anonymous-block.md) 以进一步了解查询服务中的匿名块。

匿名块子查询的运行状态左侧有选项卡。 选择一个选项卡以显示运行详细信息。

![显示匿名块查询的查询运行概述。 多个查询选项卡会突出显示。](../images/ui/monitor-queries/anonymous-block-overview.png)

如果匿名块查询失败，您可以通过此UI找到该特定块的错误代码。

![查询运行概述显示一个匿名块查询，其中突出显示了一个块的错误代码。](../images/ui/monitor-queries/anonymous-block-failed-query.png)

选择 **[!UICONTROL 查询]** 返回到“计划详细信息”屏幕，或 **[!UICONTROL 计划的查询]** 以返回 [!UICONTROL 计划的查询] 选项卡。

![突出显示“查询”的“运行详细信息”屏幕。](../images/ui/monitor-queries/return-navigation.png)
