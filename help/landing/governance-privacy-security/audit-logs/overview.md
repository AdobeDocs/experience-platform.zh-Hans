---
title: 审核日志概述
description: 了解您如何借助审核日志看到谁在 Adobe Experience Platform 中执行了哪些操作。
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: cf6ff8bcd3dfebe551ac3d7289fa8d5fb2a78079
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 25%

---

# 审核日志 {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="热门操作"
>abstract="此构件显示在所选时间范围内在Experience Platform中执行的操作的前几种。 要查看Platform中记录的操作的完整列表，请选择 **审核** 左侧导航栏中。"

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="顶级用户"
>abstract="此构件显示在选定的时间范围内在Experience Platform中执行了最多操作的用户。 要查看Platform中记录的操作的完整列表，请选择 **审核** 左侧导航栏中。"

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="描述"
>abstract=""

为了提高系统中所执行活动的透明度和可见性，Adobe Experience Platform允许您以“审核日志”的形式审核各种服务和功能的用户活动。 这些日志形成审核记录，可以帮助解决Platform上的问题，并帮助您的企业有效地遵守公司数据管理政策和法规要求。

从基本意义上讲，审核日志将说明&#x200B;**谁**&#x200B;执行了&#x200B;**什么**&#x200B;操作，以及在&#x200B;**什么时候**&#x200B;执行的。日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。

本文档介绍了Platform中的审核日志，包括如何在UI或API中查看和管理它们。

## 审核日志记录的事件类型 {#category}

下表概述了审核日志针对哪些资源记录了哪些操作：

| 资源 | 操作 |
| --- | --- |
| [访问控制策略（基于属性的访问控制）](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [帐户(Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [Attribution AI实例](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li></ul> |
| [审核日志](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>导出</li></ul> |
| [类](../../../xdm/schema/composition.md#class) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [计算属性](../../../profile/computed-attributes/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [客户人工智能实例](../../../intelligent-services/customer-ai/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li></ul> |
| [数据集](../../../catalog/datasets/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>为以下对象启用 [Real-time Customer Profile](../../../profile/home.md)</li><li>为配置文件禁用</li><li>添加数据</li><li>删除批次</li></ul> |
| [数据流](../../../edge/datastreams/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li><li>[编辑映射](../../../edge/datastreams/data-prep.md)</li></ul> |
| [数据类型](../../../xdm/schema/composition.md#data-type) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [目标](../../../destinations/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li><li>数据集激活</li><li>数据集移除</li><li>配置文件激活</li><li>配置文件删除</li></ul> |
| [字段组](../../../xdm/schema/composition.md#field-group) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [身份图](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>视图</li></ul> |
| [身份命名空间](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>创建</li><li>更新</li></ul> |
| [合并策略](../../../profile/merge-policies/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [产品配置文件](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [查询](../../../query-service/ui/overview.md) | <ul><li>Execute</li></ul> |
| [查询模板](../../../query-service/ui/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [角色（基于属性的访问控制）](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>添加用户</li><li>删除用户</li></ul> |
| [沙盒](../../../sandboxes/home.md) | <ul><li>创建</li><li>更新</li><li>重置</li><li>Delete</li></ul> |
| [计划的查询](../../../query-service/ui/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [架构](../../../xdm/schema/composition.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>为配置文件启用</li></ul> |
| [区段](../../../segmentation/home.md) | <ul><li>创建</li><li>Delete</li><li>区段激活</li><li>区段移除</li></ul> |
| [源数据流](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li><li>数据集激活</li><li>数据集移除</li><li>配置文件激活</li><li>配置文件移除</li></ul> |
| [工单](../../../hygiene/home.md) | <ul><li>创建</li></ul> |

## 访问审核日志

为您的组织启用该功能后，系统会在活动发生时自动收集审核日志。您无需手动启用日志收集。

要查看和导出审核日志，您必须具有 **[!UICONTROL 查看用户活动日志]** 已授予访问控制权限(可在 [!UICONTROL 数据管理] 类别)。 要了解如何管理Platform功能的各个权限，请参阅 [访问控制文档](../../../access-control/home.md).

## 在UI中管理审核日志 {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="说明"
>abstract=""

您可以在中查看各种Experience Platform功能的审核日志 **[!UICONTROL 审核]** Platform UI中的工作区。 工作区会显示记录的日志列表，默认情况下按从最近到最近排序。

![审核日志仪表板](../../images/audit-logs/audits.png)

审核日志会保留365天，之后将从系统中删除它们。 因此，返回的时间最多只能为365天。 如果您需要的数据超过365天，则应定期导出日志以满足内部策略要求。

从列表中选择一个事件，即可在右边栏中查看其详细信息。

![事件详细信息](../../images/audit-logs/select-event.png)

### 筛选审核日志

>[!NOTE]
>
>由于这是一项新功能，显示的数据仅追溯到2022年3月。 根据所选资源，从2022年1月起，可能会提供以前的数据。


选择漏斗图标(![过滤器图标](../../images/audit-logs/icon.png))，以显示过滤器控件列表以帮助缩小结果范围。 仅显示最后1000条记录，这与选择的各种过滤器无关。

![筛选器](../../images/audit-logs/filters.png)

在 UI 中有以下过滤器可用于审核事件：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 类别] | 使用下拉菜单按以下条件筛选显示的结果 [类别](#category). |
| [!UICONTROL 操作] | 按操作筛选。 当前仅限 [!UICONTROL 创建] 和 [!UICONTROL 删除] 可以筛选操作。 |
| [!UICONTROL 用户] | 输入完整的用户ID(例如， `johndoe@acme.com`)，以按用户筛选。 |
| [!UICONTROL 状态] | 按操作是允许（完成）还是由于缺少而拒绝进行筛选 [访问控制](../../../access-control/home.md) 权限。 |
| [!UICONTROL 日期] | 选择开始日期和/或结束日期，以定义筛选结果的日期范围。 可导出90天回顾期的数据（例如，从2021-12-15到2022-03-15）。 这可能因事件类型而异。 |

要移除过滤器，请选择相关过滤器的药丸图标上的“X”，或选择 **[!UICONTROL 全部清除]** 以删除所有筛选器。

![清除筛选器](../../images/audit-logs/clear-filters.png)

### 导出审核日志

要导出审核日志的当前列表，请选择 **[!UICONTROL 下载日志]**.

![下载日志](../../images/audit-logs/download.png)

在显示的对话框中，选择您首选的格式(可以 **[!UICONTROL CSV]** 或 **[!UICONTROL JSON]**)，然后选择 **[!UICONTROL 下载]**. 浏览器下载生成的文件，并将其保存到您的计算机。

![选择下载格式](../../images/audit-logs/select-download-format.png)

## 在API中管理审核日志

您在 UI 中可以执行的所有操作也可以使用 API 调用来完成。有关详细信息，请参阅 [ API 参考文档](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的审核日志

要了解如何管理Adobe Admin Console中的活动的审核日志，请参阅以下内容 [文档](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## 后续步骤和其他资源

本指南介绍了如何管理Experience Platform中的审核日志。 有关如何监视Platform活动的更多信息，请参阅以下文档： [可观察性洞察](../../../observability/home.md) 和 [监测数据摄取](../../../ingestion/quality/monitor-data-ingestion.md).

要加深您对Experience Platform中审核日志的了解，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
