---
title: 查询日志
description: 每次执行查询时都会自动生成查询日志，可以通过UI帮助进行疑难解答。 本文档概述了如何使用及导航UI的“查询服务日志”部分。
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---

# 查询日志

Adobe Experience Platform维护通过API和UI发生的所有查询事件的日志。 此信息可在[!UICONTROL 日志]选项卡的查询服务UI中获取。

日志文件由任何查询事件自动生成，并包含所使用的SQL、查询状态、所用时间和上次运行时间等信息。 您可以使用查询日志数据作为功能强大的工具，来排查查询效率低下或存在问题的情况。 更全面的日志信息作为审核日志功能的一部分保留，可以在[审核日志文档](../../landing/governance-privacy-security/audit-logs/overview.md)中找到。

## 检查查询日志 {#check-query-logs}

要检查查询日志，请选择[!UICONTROL 查询]导航到查询服务工作区，然后从可用选项中选择[!UICONTROL 日志]。

>[!NOTE]
>
>默认情况下，系统查询和仪表板查询都被排除。 有关如何根据您的设置优化显示的日志的信息，请参阅[筛选器](#filter-logs)部分。

![突出显示查询和日志的Experience Platform UI。](../images/ui/query-log/logs.png)

## 自定义和搜索 {#customize-and-search}

查询服务日志以可自定义的表格式提供。 要自定义表格列，请选择设置图标（![A设置图标）。](/help/images/icons/column-settings.png))。 将显示[!UICONTROL 自定义表]对话框，其中可以取消选择每个列。

您还可以通过在搜索字段中键入模板名称来搜索与特定查询模板相关的日志。

![查询日志工作区，其搜索栏和管理列表下拉列表突出显示。](../images/ui/query-log/customize-logs.png)

可以在查询服务概述的“日志”部分中找到每个日志表列[&#128279;](./overview.md#log)的描述。

## 发现日志数据

每一行表示与查询模板关联的查询运行的日志数据。 从表中选择任意行以使用运行日志数据填充右侧边栏。

![查询日志工作区中选定了一行，右侧边栏中的日志数据突出显示。](../images/ui/query-log/log-details.png)

在日志详细信息面板中，您可以执行各种操作。 您可以以CTAS身份运行查询，这会创建新的输出数据集，查看或复制运行中使用的完整SQL查询，或删除该查询。

>[!NOTE]
>
>[!UICONTROL 以CTAS运行]的选项仅适用于SELECT查询。

![查询日志工作区中选定一行，运行为CTAS，删除查询并突出显示复制SQL图标。](../images/ui/query-log/edit-output-dataset.png)

您还可以从[!UICONTROL 名称]列中选择查询模板名称，以直接导航到[!UICONTROL 查询日志详细信息]视图。

>[!NOTE]
>
>如果查询是使用API创建的，并且在初始化期间未提供模板名称，则会显示SQL查询的前几十个字符。

![查询日志详细信息视图。](../images/ui/query-log/query-log-details.png)

## 编辑日志 {#edit-logs}

每行的模板名称或SQL代码片段旁边是一个铅笔图标（![铅笔图标）。](/help/images/icons/edit.png))，可用于导航到查询编辑器。 然后，在编辑器中预填充该查询以进行编辑。

![查询日志工作区中铅笔图标突出显示。](../images/ui/query-log/edit-query.png)

## 筛选日志 {#filter-logs}

您可以根据各种设置筛选查询日志列表。 选择过滤器图标(![过滤器图标。](/help/images/icons/filter.png))，以在左边栏中打开一组筛选器选项。

![查询日志工作区中筛选器图标突出显示。](../images/ui/query-log/log-filter.png)

此时将显示可用筛选器列表。

![显示并突出显示筛选选项的查询日志工作区。](../images/ui/query-log/log-filter-settings.png)

下表提供了每个过滤器的说明。

| 筛选条件 | 描述 |
| ------ | ----------- |
| [!UICONTROL 排除仪表板查询] | 此复选框默认处于启用状态，它不包括用于生成分析的查询生成的日志。 这些查询是系统生成的，模糊了用户生成的日志的记录，而这些日志是监控、管理和故障排除所必需的。 要查看系统生成的日志，请取消选中复选框。 |
| [!UICONTROL 排除系统查询] | 此复选框默认处于启用状态，它不包括系统生成的日志。 系统生成的查询通常包括后台任务或维护操作，可能与用户监控、管理或故障排除目的无关。 如果需要检查系统生成的日志，请取消选中此复选框以将其包含在日志视图中。 |
| [!UICONTROL 开始日期] | 要筛选在特定期间创建的查询日志，请在[!UICONTROL 开始日期]部分中设置[!UICONTROL 开始]和[!UICONTROL 结束]日期。 |
| [!UICONTROL 完成日期] | 要筛选在特定期间完成的查询的日志，请在[!UICONTROL 完成日期]部分中设置[!UICONTROL 开始]和[!UICONTROL 结束]日期。 |
| [!UICONTROL 状态] | 要根据查询的[!UICONTROL 状态]筛选日志，请选择相应的单选按钮。 可用选项包括[!UICONTROL 已提交]、[!UICONTROL 正在进行]、[!UICONTROL 成功]和[!UICONTROL 失败]。 您一次只能基于一个状态条件筛选日志。 |
| [!UICONTROL 客户端] | 要根据使用的查询客户端筛选日志，请在自由文本字段中输入以下接受值之一： `API`、`Adobe Query Service UI`或`QsAccel`。 |
| [!UICONTROL 我的查询] | 使用[!UICONTROL 我的查询]切换功能筛选由您执行的查询日志。 |
| [!UICONTROL 查询日志ID] | 要根据查询的唯一日志ID进行筛选，请在自由文本字段中输入日志ID。 此信息可在[!UICONTROL 日志详细信息]中找到。 |

任何应用的过滤器都会显示在过滤的日志结果上方。

![查询工作区的“日志”选项卡，已应用的筛选器列表突出显示。](../images/ui/query-log/applied-log-filters.png)

## 后续步骤

通过阅读本文档，您现在可以更好地了解如何在查询服务UI中访问和使用查询日志。

请参阅[UI概述](./overview.md)或[查询服务API指南](../api/getting-started.md)，了解有关查询服务功能的更多信息。

请参阅[监视查询文档](./monitor-queries.md)，了解查询服务如何改进已计划查询运行的可见性。
