---
title: 审核日志概述
description: 了解审核日志如何让您了解谁在Adobe Experience Platform中执行了哪些操作。
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 4dc49c7219ebb613c74e5960f1f8d477dc1b7605
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 5%

---

# 审核日志（测试版）

>[!IMPORTANT]
>
>Adobe Experience Platform中的审核日志功能目前处于测试阶段。 本文档中描述的功能可能会发生更改。

为了提高系统中所执行活动的透明度和可见性，Adobe Experience Platform允许您以“审核日志”的形式审核各种服务和功能的用户活动。 这些日志形成了一个审核跟踪，可帮助解决平台上的问题，并帮助您的企业有效地遵守公司数据管理策略和法规要求。

从基本意义上讲，审核日志告知&#x200B;**谁**&#x200B;执行了&#x200B;**什么**&#x200B;操作，以及&#x200B;**何时执行**。 日志中记录的每个操作都包含元数据，这些元数据指示操作类型、日期和时间、执行操作的用户的电子邮件ID，以及与操作类型相关的其他属性。

本文档介绍Platform中的审核日志，包括如何在UI或API中查看和管理这些日志。

## 由审核日志捕获的事件类型 {#category}

下表概述了审计日志记录哪些资源的操作：

| 资源 | 操作 |
| --- | --- |
| [数据集](../../../catalog/datasets/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>为[实时客户资料](../../../profile/home.md)启用</li></ul> |
| [架构](../../../xdm/schema/composition.md) | <ul><li>创建</li><li>更新</li><li>删除</li></ul> |
| [类](../../../xdm/schema/composition.md#class) | <ul><li>创建</li><li>更新</li><li>删除</li></ul> |
| [字段组](../../../xdm/schema/composition.md#field-group) | <ul><li>创建</li><li>更新</li><li>删除</li></ul> |
| [数据类型](../../../xdm/schema/composition.md#data-type) | <ul><li>创建</li><li>更新</li><li>删除</li></ul> |
| [沙盒](../../../sandboxes/home.md) | <ul><li>创建</li><li>更新</li><li>重置</li><li>删除</li></ul> |
| [目标](../../../destinations/home.md) | <ul><li>激活</li></ul> |

## 访问审核日志

为贵组织启用该功能后，会在发生活动时自动收集审核日志。 您无需手动启用日志收集。

要查看和导出审核日志，您必须已授予“查看审核日志”访问控制权限（位于“数据管理”类别下）。 要了解如何管理Platform功能的各个权限，请参阅[访问控制文档](../../../access-control/home.md)。

## 在UI中管理审核日志

您可以在Platform UI的&#x200B;**[!UICONTROL Audits]**&#x200B;工作区中查看不同Experience Platform功能的审核日志。 工作区会显示记录日志的列表，默认情况下，该列表按从最近到最近的顺序进行排序。

![审核日志仪表板](../../images/audit-logs/audits.png)

系统仅显示去年的审核日志。 超出此限制的任何日志将自动从系统中删除。

从列表中选择事件，以在右边栏中查看其详细信息。

![事件详细信息](../../images/audit-logs/select-event.png)

选择漏斗图标（![过滤器图标](../../images/audit-logs/icon.png)）可显示过滤器控件列表，以帮助缩小结果范围。

![筛选器](../../images/audit-logs/filters.png)

以下过滤器可用于UI中的审核事件：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 类别] | 使用下拉菜单按[category](#category)筛选显示的结果。 |
| [!UICONTROL 操作] | 按操作过滤。 当前只能过滤[!UICONTROL Create]和[!UICONTROL Delete]操作。 |
| [!UICONTROL 访问控制状态] | 按以下方式进行筛选：由于缺少[访问控制](../../../access-control/home.md)权限，是允许（已完成）还是拒绝该操作。 |
| [!UICONTROL 日期] | 选择开始日期和/或结束日期，以定义日期范围以按过滤结果。 |

要删除过滤器，请在相关过滤器的“药丸”图标上选择“X”，或选择&#x200B;**[!UICONTROL 全部清除]**&#x200B;以删除所有过滤器。

![清除过滤器](../../images/audit-logs/clear-filters.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## 在API中管理审核日志

您可以在UI中执行的所有操作也可以使用API调用来完成。 有关更多信息，请参阅[API参考文档](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的审核日志

要了解如何管理Adobe Admin Console中活动的审核日志，请参阅以下[document](https://helpx.adobe.com/enterprise/using/audit-logs.html)。

## 后续步骤

本指南介绍了如何在Experience Platform中管理审核日志。 有关如何监控Platform活动的更多信息，请参阅[可观察性分析](../../../observability/home.md)和[监控数据摄取](../../../ingestion/quality/monitor-data-ingestion.md)的文档。
