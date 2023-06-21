---
title: 监视计划查询
description: 了解如何通过查询服务UI监控查询。
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 75ef9c58aa7c5f1cc628d1f13b6c5f56b362458a
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---

# 监视计划查询

Adobe Experience Platform通过UI提高了所有查询作业状态的可见性。 从 [!UICONTROL 计划的查询] 选项卡，您现在可以找到有关查询运行的重要信息，包括状态、计划详细信息以及失败时的错误消息/代码。 您还可以通过UI为任何此类查询订阅基于其状态的查询警报，方法是使用 [!UICONTROL 计划的查询] 选项卡。

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
| **[!UICONTROL 名称]** | 名称字段是模板名称或SQL查询的前几个字符。 使用查询编辑器通过UI创建的任何查询都会在开始时命名。 如果查询是通过API创建的，则其名称将成为用于创建查询的初始SQL的片段。 要查看与查询关联的所有运行的列表，请从中选择一项 [!UICONTROL 名称] 列。 欲了解更多信息，请参见 [查询运行计划详细信息](#query-runs) 部分。 |
| **[!UICONTROL 模板]** | 查询的模板名称。 选择模板名称以导航到“查询编辑器”。 为方便起见，查询编辑器中会显示查询模板。 如果没有模板名称，该行将标有连字符，并且无法重定向到查询编辑器以查看查询。 |
| **[!UICONTROL SQL]** | SQL查询的片段。 |
| **[!UICONTROL 运行频率]** | 查询设置为运行的节奏。 可用的值包括 `Run once` 和 `Scheduled`. 可以根据查询的运行频率对其进行筛选。 |
| **[!UICONTROL 创建者]** | 创建查询的用户的名称。 |
| **[!UICONTROL 已创建]** | 创建查询时的时间戳（UTC格式）。 |
| **[!UICONTROL 上次运行时间戳]** | 运行查询时的最新时间戳。 此列突出显示查询是否已根据其当前计划执行。 |
| **[!UICONTROL 上次运行状态]** | 最近查询执行的状态。 状态值包括： `Success`， `Failed`， `In progress`、和 `No runs`. |
| **[!UICONTROL 计划状态]** | 计划查询的当前状态。 有五个潜在值， [!UICONTROL 正在注册]， [!UICONTROL 活动]， [!UICONTROL 不活动]， [!UICONTROL 已删除]和连字符。 <ul><li>连字符表示计划的查询是一次性的非循环查询。</li><li>此 [!UICONTROL 正在注册] 状态表示系统仍在为查询创建新计划。 注意，您不能在注册时禁用或删除计划查询。</li><li>此 [!UICONTROL 活动] 状态表示计划查询具有 **尚未通过** 完成日期和时间。</li><li>此 [!UICONTROL 不活动] 状态表示计划查询具有 **已通过** 完成日期和时间。</li><li>此 [!UICONTROL 已删除] 状态表示查询计划已删除。</li></ul> |

>[!TIP]
>
>如果导航到查询编辑器，则可以选择 **[!UICONTROL 查询]** 以返回 [!UICONTROL 模板] 选项卡。

## 自定义计划查询的表设置 {#customize-table}

您可以调整上的列 [!UICONTROL 计划的查询] 轻松满足您的需求。 打开 [!UICONTROL 自定义表] 设置对话框并编辑可用列，选择设置图标(![设置图标。](../images/ui/monitor-queries/settings-icon.png))。

>[!NOTE]
>
>此 [!UICONTROL 已创建] 默认情况下，引用计划创建日期的列处于隐藏状态。

![突出显示“自定义表格设置”图标的“计划查询”选项卡。](../images/ui/monitor-queries/customze-table-settings-icon.png)

切换相关的复选框以删除或添加表列。 接下来，选择 **[!UICONTROL 应用]** 以确认您的选择。

>[!NOTE]
>
>通过UI创建的任何查询都将在创建过程中成为命名模板。 模板名称显示在模板列中。 如果查询是通过API创建的，则模板列为空。

![自定义表设置对话框。](../images/ui/monitor-queries/customize-table-dialog.png)

## 使用内联操作管理计划查询 {#inline-actions}

此 [!UICONTROL 计划的查询] 查看提供各种内联操作，以便从一个位置管理所有计划的查询。 每行中都会显示内联操作，并带有省略号。 选择要管理的计划查询的省略号，以在弹出菜单中查看可用选项。 可用选项包括 [[!UICONTROL 禁用计划]](#disable) 或 [!UICONTROL 启用计划]， [[!UICONTROL 删除计划]](#delete)、和 [[!UICONTROL 订阅]](#alert-subscription) 以查询警报。

![选中了内联操作省略号和弹出菜单的“计划查询”选项卡。](../images/ui/monitor-queries/disable-inline.png)

### 禁用或启用计划查询 {#disable}

要禁用计划查询，请选择要管理的计划查询的省略号，然后选择 **[!UICONTROL 禁用计划]** 从弹出菜单中的选项中进行选择。 将显示一个对话框以确认您的操作。 选择 **[!UICONTROL 禁用]** 以确认设置。

禁用计划查询后，您可以通过同一进程启用计划。 选择省略号，然后选择 **[!UICONTROL 启用计划]** 从可用选项开始。

### 删除计划查询 {#delete}

要删除计划查询，请选择要管理的计划查询的省略号，然后选择 **[!UICONTROL 删除计划]** 从弹出菜单中的选项中进行选择。 将显示一个对话框以确认您的操作。 选择 **[!UICONTROL 删除]** 以确认设置。

删除计划查询后，它会 **非** 已从计划查询列表中删除。 省略号提供的内联操作将被删除并替换为灰显的添加警报图标。 您无法订阅已删除计划的警报。 该行保留在UI中，用于提供有关作为计划查询的一部分执行的运行的信息。

![“计划查询”选项卡，其中有一个已删除的计划查询，并且突出显示了一个灰显的警报图标。](../images/ui/monitor-queries/post-delete.png)

如果要为该查询模板计划运行，请从相应的行中选择模板名称以导航到查询编辑器，然后按照以下步骤操作 [有关向查询添加计划的说明](./query-schedules.md#create-schedule) 如文档中所述。

### 订阅警报 {#alert-subscription}

要订阅计划查询运行的警报，请选择要管理的计划查询的省略号，然后选择 **[!UICONTROL 订阅]** 从弹出菜单中的选项中进行选择。

此 [!UICONTROL 警报] 对话框打开。 此 [!UICONTROL 警报] 该对话框允许您同时订阅UI通知和电子邮件警报。 警报基于查询的状态。 有三个可用选项： `start`， `success`、和 `failure`. 选中相应的一个或多个框并选择 **[!UICONTROL 保存]** 订购。 您可以订阅警报，只要它们没有 [!UICONTROL 上次运行时间戳] 值。

![警报订阅对话框。](../images/ui/monitor-queries/alert-subscription-dialog.png)

请参阅 [警报订阅API文档](../api/alert-subscriptions.md) 了解更多信息。

### 查看查询详细信息 {#query-details}

选择信息图标(![信息图标。](../images/ui/monitor-queries/information-icon.png))，以查看查询的详细信息面板。 详细信息面板包含有关查询的所有相关信息，但不包括计划查询表中包含的事实信息。 其他信息包括查询ID、上次修改日期、查询的SQL、计划ID和当前设置的计划。

![“计划查询”选项卡，其中信息图标和详细信息面板突出显示。](../images/ui/monitor-queries/details-panel.png)

## 筛选查询 {#filter}

您可以根据运行频率筛选查询。 从 [!UICONTROL 计划的查询] 选项卡，选择过滤器图标(![过滤器图标](../images/ui/monitor-queries/filter-icon.png))以打开过滤器侧栏。

![突出显示过滤器图标的计划查询选项卡。](../images/ui/monitor-queries/filter-queries.png)

要根据查询的运行频率筛选查询列表，请选择 **[!UICONTROL 已计划]** 或 **[!UICONTROL 运行一次]** 筛选复选框。

>[!NOTE]
>
>任何已执行但未计划的查询均符合 [!UICONTROL 运行一次].

![突出显示过滤器侧栏的计划查询选项卡。](../images/ui/monitor-queries/filter-sidebar.png)

启用筛选条件后，选择 **[!UICONTROL 隐藏筛选器]** 以关闭过滤器面板。

## 查询运行计划详细信息 {#query-runs}

要打开“调度详细资料”页，请从中选择一个查询名称 [!UICONTROL 计划的查询] 选项卡。 此视图提供在该计划查询中执行的所有运行的列表。 提供的信息包括开始和结束时间、状态以及所使用的数据集。

![“调度详细资料”页。](../images/ui/monitor-queries/schedule-details.png)

此信息以五列表格形式提供。 每一行表示查询执行。

| 列名称 | 描述 |
|---|---|
| **[!UICONTROL 查询运行Id]** | 每日执行的查询运行ID。 选择 **[!UICONTROL 查询运行Id]** 导航到 [!UICONTROL 查询运行概述]. |
| **[!UICONTROL 查询运行开始]** | 执行查询的时间戳。 时间戳采用UTC格式。 |
| **[!UICONTROL 查询运行完成]** | 查询完成时的时间戳。 时间戳采用UTC格式。 |
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

您可以从此视图将查询SQL复制到剪贴板。 要复制查询，请选择SQL代码片段右上角的复制图标。 此时会显示一条弹出消息，确认代码已被复制。

![突出显示SQL复制图标的运行详细信息屏幕。](../images/ui/monitor-queries/copy-sql.png)

### 使用匿名块运行查询的详细信息 {#anonymous-block-queries}

使用匿名块组成其SQL语句的查询被分隔到其各个子查询中。 子查询中的分隔允许您单独检查每个查询块的运行详细信息。

>[!NOTE]
>
>使用DROP命令的匿名块的运行详细信息将 **非** 将作为单独的子查询报告。 CTAS查询、ITAS查询和用作匿名块子查询的COPY语句有单独的运行详细信息。 当前不支持DROP命令的运行详细信息。

匿名块通过使用 `$$` 在查询前添加前缀。 要了解有关查询服务中匿名块的更多信息，请参阅 [匿名阻止文档](../essential-concepts/anonymous-block.md).

匿名块子查询的运行状态左侧有选项卡。 选择一个选项卡以显示运行详细信息。

![显示匿名块查询的查询运行概述。 多个查询选项卡会突出显示。](../images/ui/monitor-queries/anonymous-block-overview.png)

如果匿名块查询失败，您可以通过此UI找到该特定块的错误代码。

![查询运行概述显示一个匿名块查询，其中突出显示了一个块的错误代码。](../images/ui/monitor-queries/anonymous-block-failed-query.png)

选择 **[!UICONTROL 查询]** 返回到“计划详细信息”屏幕，或 **[!UICONTROL 计划的查询]** 以返回 [!UICONTROL 计划的查询] 选项卡。

![突出显示“查询”的“运行详细信息”屏幕。](../images/ui/monitor-queries/return-navigation.png)

<!-- Details required to complete this section below:
### Run details for queries with parameterized queries {#parameterized-queries}

Queries that use parameterized values to make up the SQL statement are ... 
-->
