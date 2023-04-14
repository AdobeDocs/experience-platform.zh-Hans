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

Adobe Experience Platform通过UI改善了所有查询作业状态的可见性。 从 [!UICONTROL 计划查询] 选项卡现在可以查找有关查询运行的重要信息，包括状态、计划详细信息以及失败时的错误消息/代码。 您还可以通过UI，为通过的任何这些查询订阅基于状态的警报 [!UICONTROL 计划查询] 选项卡。

## [!UICONTROL 计划查询]

的 [!UICONTROL 计划查询] 选项卡提供了所有计划CTAS和ITAS查询的概述。 可以找到所有计划查询的运行详细信息，以及任何失败查询的错误代码和消息。

导航到 [!UICONTROL 计划查询] 选项卡，选择 **[!UICONTROL 查询]** 从左侧导航栏中，然后是 **[!UICONTROL 计划查询]**

![“查询”工作区中的“计划查询”选项卡。](../images/ui/monitor-queries/scheduled-queries.png)

下表描述了每个可用列。

>[!NOTE]
>
>警报订阅图标包含在未命名列的每一行中。 请参阅 [警报订阅](#alert-subscription) 的子菜单。

| 栏目 | 描述 |
|---|---|
| **[!UICONTROL 名称]** | 名称字段是模板名称或SQL查询的前几个字符。 任何通过具有查询编辑器的UI创建的查询，在开始时即会命名。 如果查询是通过API创建的，则其名称将变为用于创建查询的初始SQL的代码段。 从 [!UICONTROL 名称] 列，查看与查询关联的所有运行的列表。 有关详细信息，请参阅 [查询运行计划详细信息](#query-runs) 中。 |
| **[!UICONTROL 模板]** | 查询的模板名称。 选择模板名称以导航到查询编辑器。 为方便起见，查询模板会显示在查询编辑器中。 如果没有模板名称，则该行将标有连字符，并且无法重定向到查询编辑器以查看查询。 |
| **[!UICONTROL SQL]** | SQL查询的代码段。 |
| **[!UICONTROL 运行频率]** | 这是设置查询运行的频率。 可用值包括 `Run once` 和 `Scheduled`. 可以根据查询的运行频率对查询进行筛选。 |
| **[!UICONTROL 创建者]** | 创建查询的用户的名称。 |
| **[!UICONTROL 已创建]** | 以UTC格式创建查询时的时间戳。 |
| **[!UICONTROL 上次运行时间戳]** | 运行查询时的最近时间戳。 此列突出显示查询是否已根据其当前计划执行。 |
| **[!UICONTROL 上次运行状态]** | 最近一次查询执行的状态。 状态值为： `Success`, `Failed`, `In progress`和 `No runs`. |

>[!TIP]
>
>如果导航到查询编辑器，则可以选择 **[!UICONTROL 查询]** 返回 [!UICONTROL 模板] 选项卡。

### 自定义计划查询的表设置

您可以在 [!UICONTROL 计划查询] 选项卡。 选择设置图标(![设置图标。](../images/ui/monitor-queries/settings-icon.png))以打开 [!UICONTROL 自定义表] 设置对话框和编辑可用列。

![自定义表设置图标。](../images/ui/monitor-queries/customze-table-settings-icon.png)

切换相关复选框以删除或添加表列。 接下来，选择 **[!UICONTROL 应用]** 以确认您的选择。

>[!NOTE]
>
>通过UI创建的任何查询都将成为创建过程中命名的模板。 模板名称显示在模板列中。 如果查询是通过API创建的，则模板列为空。

![“自定义表设置”对话框。](../images/ui/monitor-queries/customize-table-dialog.png)

### 订阅警报 {#alert-subscription}

您可以订阅 [!UICONTROL 计划查询] 选项卡。 选择警报通知图标(![警报图标。](../images/ui/monitor-queries/alerts-icon.png))以打开 [!UICONTROL 警报] 对话框。 的 [!UICONTROL 警报] 对话框同时订阅了UI通知和电子邮件警报。 警报基于查询的状态。 有三个选项可用： `start`, `success`和 `failure`. 选中相应的框并选择 **[!UICONTROL 保存]** 订阅。

![警报订阅对话框。](../images/ui/monitor-queries/alert-subscription-dialog.png)

请参阅 [警报订阅API文档](../api/alert-subscriptions.md) 以了解更多信息。

### 筛选查询 {#filter}

您可以根据运行频率过滤查询。 从 [!UICONTROL 计划查询] ，选择过滤器图标(![过滤器图标](../images/ui/monitor-queries/filter-icon.png))以打开过滤器侧栏。

![“计划查询”选项卡突出显示了过滤器图标。](../images/ui/monitor-queries/filter-queries.png)

选择 **[!UICONTROL 已计划]** 或 **[!UICONTROL 运行一次]** 运行频率筛选器复选框以筛选查询列表。

>[!NOTE]
>
>已执行但未计划符合条件的任何查询 [!UICONTROL 运行一次].

![计划查询选项卡，过滤器侧栏突出显示。](../images/ui/monitor-queries/filter-sidebar.png)

启用过滤器标准后，选择 **[!UICONTROL 隐藏过滤器]** 来关闭过滤器面板。

## 查询运行计划详细信息 {#query-runs}

选择查询名称以导航到计划详细信息页面。 此视图提供作为计划查询的一部分执行的所有运行的列表。 提供的信息包括使用的开始和结束时间、状态和数据集。

![计划详细信息页面。](../images/ui/monitor-queries/schedule-details.png)

此信息在五列表中提供。 每行表示查询执行。

| 列名称 | 描述 |
|---|---|
| **[!UICONTROL 查询运行ID]** | 每天执行的查询运行ID。 选择 **[!UICONTROL 查询运行ID]** 导航到 [!UICONTROL 查询运行概述]. |
| **[!UICONTROL 查询运行开始]** | 执行查询时的时间戳。 采用UTC格式。 |
| **[!UICONTROL 查询运行结束]** | 查询完成时的时间戳。 采用UTC格式。 |
| **[!UICONTROL 状态]** | 最近一次查询执行的状态。 三个状态值是： `successful` `failed` 或 `in progress`. |
| **[!UICONTROL 数据集]** | 执行中涉及的数据集。 |

计划查询的详细信息可在 [!UICONTROL 属性] 的上界。 此面板包括初始查询ID、客户端类型、模板名称、查询SQL和计划的终止时间。

![“计划详细信息”页面中，“属性”面板突出显示。](../images/ui/monitor-queries/properties-panel.png)

选择查询运行ID以导航到运行详细信息页面并查看查询信息。

![运行ID突出显示的计划详细信息屏幕。](../images/ui/monitor-queries/navigate-to-run-details.png)

## 查询运行概述 {#query-run-overview}

的 [!UICONTROL 查询运行概述] 提供有关此计划查询的单个运行的信息，以及运行状态的更详细划分。 此页面还包含客户端信息以及可能导致查询失败的任何错误的详细信息。

![“运行详细信息”屏幕中突出显示了“概述”部分。](../images/ui/monitor-queries/query-run-details.png)

如果查询失败，查询状态部分将提供错误代码和错误消息。

![“运行详细信息”屏幕中突出显示了“错误”部分。](../images/ui/monitor-queries/failed-query.png)

可以从此视图将查询SQL复制到剪贴板。 选择SQL代码段右上角的复制图标以复制查询。 弹出消息确认代码已复制。

![运行详细信息屏幕中突出显示了SQL复制图标。](../images/ui/monitor-queries/copy-sql.png)

### 运行具有匿名块的查询的详细信息 {#anonymous-block-queries}

使用匿名块组成其SQL语句的查询被分隔成各自的子查询。 这允许您单独检查每个查询块的运行详细信息。

>[!NOTE]
>
>使用DROP命令的匿名块的运行详细信息将 **not** 作为单独的子查询报告。 对于CTAS查询、ITAS查询和用作匿名块子查询的COPY语句，可以使用单独的运行详细信息。 当前不支持DROP命令的运行详细信息。

匿名块通过使用 `$$` 前缀。 请参阅 [匿名块文档](../essential-concepts/anonymous-block.md) 以详细了解查询服务中的匿名块。

匿名块子查询在运行状态的左侧具有选项卡。 选择一个选项卡以显示运行详细信息。

![“查询”运行概述显示一个匿名块查询。 多个查询选项卡会突出显示。](../images/ui/monitor-queries/anonymous-block-overview.png)

如果匿名块查询失败，您可以通过此UI找到该特定块的错误代码。

![“查询”运行概述显示匿名块查询，其中突出显示单个块的错误代码。](../images/ui/monitor-queries/anonymous-block-failed-query.png)

选择 **[!UICONTROL 查询]** 返回到计划详细信息屏幕，或 **[!UICONTROL 计划查询]** 返回 [!UICONTROL 计划查询] 选项卡。

![“运行详细信息”屏幕中突出显示了“查询”。](../images/ui/monitor-queries/return-navigation.png)
