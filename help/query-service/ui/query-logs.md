---
title: 查询日志
description: 每次执行查询时都会自动生成查询日志，并且查询日志可通过UI用于帮助进行故障诊断。 本文档概述了如何使用和导航UI的查询服务日志部分。
source-git-commit: 22deca5f9bcf6bcf97cca01b97fce9d22800b767
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 查询日志

Adobe Experience Platform会维护一个日志，其中包含通过API和UI发生的所有查询事件。 此信息可在查询服务UI中(从 [!UICONTROL 日志] 选项卡。

日志文件由任何查询事件自动生成，其中包含的信息包括使用的SQL、查询的状态、所用的时长以及上次运行时间。 查询日志数据可用作对低效或问题查询进行故障诊断的强大工具。 更全面的日志信息将作为审核日志功能的一部分保留，可在 [审核日志文档](../../landing/governance-privacy-security/audit-logs/overview.md).

## 检查查询日志

要检查查询日志，请选择 [!UICONTROL 查询] 导航到“查询服务”工作区并选择 [!UICONTROL 日志] 中。

![突出显示了“查询和日志”的Platform UI。](../images/ui/query-log/logs.png)

## 自定义和搜索 {#customize-and-search}

查询服务日志以可自定义的表格式显示。 要自定义表列，请选择设置图标(![设置图标。](../images/ui/query-log/settings-icon.png))来访问Advertising Cloud的帮助。 A [!UICONTROL 自定义表] 将显示一个对话框，其中可取消选择每列。

您还可以通过在搜索字段中键入模板名称来搜索与特定查询模板相关的日志。

![突出显示了“查询日志”工作区的搜索栏和“管理列表”下拉列表。](../images/ui/query-log/customize-logs.png)

A [每个日志表列的描述](./overview.md#log) 可在查询服务概述的日志部分找到。

## 发现日志数据

每一行表示与查询模板关联的查询运行的日志数据。 从表格中选择任意行，以使用该运行的日志数据填充右侧侧栏。

![在“查询日志”工作区中选择了一行，并在右侧侧栏中突出显示日志数据。](../images/ui/query-log/log-details.png)

在“日志详细信息”面板中，您可以选择新的输出数据集，并查看或复制运行中使用的完整SQL查询。

![选中一行的“查询日志”工作区，并突出显示输出数据集和SQL查询。](../images/ui/query-log/edit-output-dataset.png)

您还可以从 [!UICONTROL 名称] 列直接导航到 [!UICONTROL 查询日志详细信息] 中。

>[!NOTE]
>
>如果查询是使用API创建的，并且在初始化期间未提供模板名称，则会显示SQL查询的前几十个字符。

![“查询日志详细信息”视图。](../images/ui/query-log/query-log-details.png)

每行的模板名称或SQL代码片段旁边都有一个铅笔图标(![铅笔图标。](../images/ui/query-log/edit-icon.png))来导航到查询编辑器。 然后，将在编辑器中预填充查询以进行编辑。

![“查询日志”工作区中突出显示了铅笔图标。](../images/ui/query-log/edit-query.png)

## 后续步骤

通过阅读本文档，您现在可以更好地了解如何在查询服务UI中访问和使用查询日志。

请参阅 [UI概述](./overview.md)，或 [查询服务API指南](../api/getting-started.md) 以了解有关查询服务功能的更多信息。

请参阅 [监视查询文档](./monitor-queries.md) 以了解查询服务如何提高计划查询运行的可见性。
