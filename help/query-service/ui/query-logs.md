---
title: 查询日志
description: 每次执行查询时都会自动生成查询日志，并且可以通过UI帮助进行故障排除。 本文档概述了如何使用及导航UI的“查询服务日志”部分。
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---

# 查询日志

>[!IMPORTANT]
>
>某些查询日志功能当前为有限版本，并非对所有客户都可用。 在没有编辑图标的情况下，您的UI可能会以稍微不同的方式显示。 此外，选择查询名称的过程可能会导航到查询编辑器，而不是 [!UICONTROL 查询日志详细信息] 视图。

Adobe Experience Platform维护通过API和UI发生的所有查询事件的日志。 此信息可在查询服务UI中获取，网址为 [!UICONTROL 日志] 选项卡。

日志文件由任何查询事件自动生成，包含的信息包括使用的SQL、查询状态、花费的时间以及上次运行时间。 您可以将查询日志数据用作功能强大的工具，用于解决查询效率低下或存在问题的问题。 更全面的日志信息作为审核日志功能的一部分保留，可以在 [审核日志文档](../../landing/governance-privacy-security/audit-logs/overview.md).

## 检查查询日志

要检查查询日志，请选择 [!UICONTROL 查询] 导航到查询服务工作区，然后选择 [!UICONTROL 日志] 从可用选项开始。

![突出显示了带有查询和日志的Platform UI。](../images/ui/query-log/logs.png)

## 自定义和搜索 {#customize-and-search}

查询服务日志以可自定义的表格式显示。 要自定义表格列，请选择设置图标(![设置图标。](../images/ui/query-log/settings-icon.png))。 A [!UICONTROL 自定义表] 此时将显示一个对话框，其中可以取消选择每一列。

您还可以通过在搜索字段中键入模板名称来搜索与特定查询模板相关的日志。

![突出显示具有搜索栏和管理列表下拉列表的查询日志工作区。](../images/ui/query-log/customize-logs.png)

A [每个日志表列的说明](./overview.md#log) 可以在查询服务概述的Log部分找到。

## 发现日志数据

每一行表示与查询模板关联的查询运行的日志数据。 从表中选择任意行，以将该运行的日志数据填充到右侧边栏中。

![在查询日志工作区中选择了行，并突出显示右侧边栏中的日志数据。](../images/ui/query-log/log-details.png)

在“日志详细信息”面板中，您可以选择新的输出数据集，并查看或复制运行中使用的完整SQL查询。

![查询日志工作区中选定了一行，并突出显示输出数据集和SQL查询。](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>某些查询日志功能当前为有限版本，并非对所有客户都可用。

您还可以从以下位置选择查询模板名称： [!UICONTROL 名称] 列直接导航到 [!UICONTROL 查询日志详细信息] 视图。

>[!NOTE]
>
>如果查询是使用API创建的，并且在初始化期间未提供模板名称，则会显示SQL查询的前几十个字符。

![查询日志详细信息视图。](../images/ui/query-log/query-log-details.png)

每行的模板名称或SQL代码片段旁边是一个铅笔图标(![铅笔图标。](../images/ui/query-log/edit-icon.png))，可用于导航到查询编辑器。 然后，会在编辑器中预填充查询以进行编辑。

![查询日志工作区中突出显示了铅笔图标。](../images/ui/query-log/edit-query.png)

## 后续步骤

通过阅读本文档，您现在可以更好地了解如何在查询服务UI中访问和使用查询日志。

请参阅 [UI概述](./overview.md)，或 [查询服务API指南](../api/getting-started.md) 了解有关查询服务功能的更多信息。

请参阅 [监测查询文档](./monitor-queries.md) 以了解查询服务如何提高计划查询运行的可见性。
