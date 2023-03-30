---
title: 审核日志概述
description: 了解您如何借助审核日志看到谁在 Adobe Experience Platform 中执行了哪些操作。
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 48%

---

# 审核日志 {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="热门操作"
>abstract="此小部件显示在选定时间范围内在 Experience Platform 中执行的最常见操作类型。要查看 Platform 中记录的操作的完整列表，请选择左侧导航中的&#x200B;**审计**。"

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="热门用户"
>abstract="此小部件显示在所选时间段内在 Experience Platform 中执行的操作最多的用户。要查看 Platform 中记录的操作的完整列表，请选择左侧导航中的&#x200B;**审计**。"

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="在 Platform 中监测用户活动"
>abstract="<h2>描述</h2><p>您可以通过审核日志的形式监测各项 Platform 服务和功能的用户活动。这些日志构成了审核记录，记录了<b>谁</b>执行了<b>什么</b>操作以及<b>何时</b>执行的。审核日志可以帮助解决 Platform 相关问题，并帮助您的企业有效遵守公司数据管理政策和监管要求。</p>"

为了提高系统中所执行活动的透明度和可见性，Adobe Experience Platform允许您以“审核日志”的形式审核各种服务和功能的用户活动。 这些日志形成了一个审核跟踪，可帮助解决平台上的问题，并帮助您的企业有效地遵守公司数据管理策略和法规要求。

从基本意义上讲，审核日志将说明&#x200B;**谁**&#x200B;执行了&#x200B;**什么**&#x200B;操作，以及在&#x200B;**什么时候**&#x200B;执行的。日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。

本文档介绍Platform中的审核日志，包括如何在UI或API中查看和管理这些日志。

## 审核日志记录的事件类型 {#category}

下表概述了审计日志记录哪些资源的操作：

| 资源 | 操作 |
| --- | --- |
| [访问控制策略（基于属性的访问控制）](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [帐户(Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [Attribution AI实例](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li></ul> |
| [审核日志](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>导出</li></ul> |
| [类](../../../xdm/schema/composition.md#class) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [计算属性](../../../profile/computed-attributes/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [Customer AI实例](../../../intelligent-services/customer-ai/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li></ul> |
| [数据集](../../../catalog/datasets/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用 [实时客户资料](../../../profile/home.md)</li><li>为配置文件禁用</li><li>添加数据</li><li>删除批次</li></ul> |
| [数据流](../../../edge/datastreams/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li><li>[编辑映射](../../../edge/datastreams/data-prep.md)</li></ul> |
| [数据类型](../../../xdm/schema/composition.md#data-type) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [目标](../../../destinations/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li><li>数据集激活</li><li>数据集删除</li><li>配置文件激活</li><li>配置文件删除</li></ul> |
| [字段组](../../../xdm/schema/composition.md#field-group) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [身份图](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>视图</li></ul> |
| [身份命名空间](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>创建</li><li>更新</li></ul> |
| [合并策略](../../../profile/merge-policies/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [产品配置文件](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [查询](../../../query-service/ui/overview.md) | <ul><li>Execute</li></ul> |
| [查询模板](../../../query-service/ui/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [角色（基于属性的访问控制）](../../../access-control/home.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>添加用户</li><li>删除用户</li></ul> |
| [沙盒](../../../sandboxes/home.md) | <ul><li>创建</li><li>更新</li><li>重置</li><li>Delete</li></ul> |
| [计划查询](../../../query-service/ui/overview.md) | <ul><li>创建</li><li>更新</li><li>Delete</li></ul> |
| [架构](../../../xdm/schema/composition.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>为配置文件启用</li></ul> |
| [区段](../../../segmentation/home.md) | <ul><li>创建</li><li>Delete</li><li>区段激活</li><li>区段删除</li></ul> |
| [源数据流](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>创建</li><li>更新</li><li>Delete</li><li>启用</li><li>禁用</li><li>数据集激活</li><li>数据集删除</li><li>用户档案激活</li><li>配置文件删除</li></ul> |
| [工作顺序](../../../hygiene/home.md) | <ul><li>创建</li></ul> |

## 访问审核日志

为您的组织启用该功能后，系统会在活动发生时自动收集审核日志。您无需手动启用日志收集。

要查看和导出审核日志，您必须具有 **[!UICONTROL 查看用户活动日志]** 已授予的访问控制权限(位于 [!UICONTROL 数据管理] 类别)。 要了解如何管理平台功能的各个权限，请参阅 [访问控制文档](../../../access-control/home.md).

## 在UI中管理审核日志 {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="说明"
>abstract="<ul><li>选择左侧导航中的<b>审核</b>。“审核”工作区显示记录的日志列表，默认情况下日志从最近到最早进行排序。</li>   <li> 注意：审核日志会保留 365 天，之后将从系统中删除。因此，您最多只能回看 365 天的日志。如果您需要回看超过 365 天的数据，则应定期导出日志以满足您的内部政策要求。 </li><li>从列表中选择一个事件以在右侧边栏中查看其详细信息。 </li><li>选择漏斗图标以显示过滤器控件列表，帮助缩小结果范围。仅显示最后 1000 条记录，这与选择的过滤器无关。 </li><li>要导出当前的审核日志列表，请选择&#x200B;**下载日志**。</li><li>有关此功能的更多帮助，请参阅 Experience League 上的<a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=zh-Hans">审核日志概述</a>。</li></ul>"

您可以在 **[!UICONTROL 审核]** 工作区。 工作区会显示记录日志的列表，默认情况下，该列表按从最近到最近的顺序进行排序。

![审核日志仪表板](../../images/audit-logs/audits.png)

审核日志会保留365天，之后这些日志将从系统中删除。 因此，您最多只能回看 365 天的日志。如果您需要超过365天的数据，则应当以常规频率导出日志，以满足内部策略要求。

从列表中选择一个事件以在右侧边栏中查看其详细信息。

![事件详细信息](../../images/audit-logs/select-event.png)

### 筛选审核日志

>[!NOTE]
由于这是一项新功能，因此显示的数据只能追溯到2022年3月。 根据所选的资源，以前的数据可能从2022年1月开始提供。


选择漏斗图标(![“过滤器”图标](../../images/audit-logs/icon.png))以显示筛选器控件列表，以帮助缩小结果范围。 无论选择何种过滤器，都只显示最后1000条记录。

![筛选器](../../images/audit-logs/filters.png)

在 UI 中有以下过滤器可用于审核事件：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 类别] | 使用下拉菜单按 [类别](#category). |
| [!UICONTROL 操作] | 按操作过滤。 当前仅 [!UICONTROL 创建] 和 [!UICONTROL 删除] 可以过滤操作。 |
| [!UICONTROL 用户] | 输入完整的用户ID(例如， `johndoe@acme.com`)来按用户进行筛选。 |
| [!UICONTROL 状态] | 按是否允许（完成）或由于缺少而拒绝该操作进行过滤 [访问控制](../../../access-control/home.md) 权限。 |
| [!UICONTROL 日期] | 选择开始日期和/或结束日期，以定义日期范围以按过滤结果。 可以使用90天的回顾期(例如，从2021-12-15到2022-03-15)导出数据。 这可能因事件类型而异。 |

要删除过滤器，请在相关过滤器的“药丸”图标上选择“X”，或选择 **[!UICONTROL 全部清除]** 删除所有过滤器。

![清除过滤器](../../images/audit-logs/clear-filters.png)

### 导出审核日志

要导出当前的审核日志列表，请选择&#x200B;**[!UICONTROL 下载日志]**。

![下载日志](../../images/audit-logs/download.png)

在显示的对话框中，选择您的首选格式( **[!UICONTROL CSV]** 或 **[!UICONTROL JSON]**)，然后选择 **[!UICONTROL 下载]**. 浏览器将下载生成的文件并将其保存到您的计算机。

![选择下载格式](../../images/audit-logs/select-download-format.png)

## 在API中管理审核日志

您在 UI 中可以执行的所有操作也可以使用 API 调用来完成。有关详细信息，请参阅 [ API 参考文档](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 管理Adobe Admin Console的审核日志

要了解如何管理Adobe Admin Console中活动的审核日志，请参阅以下内容 [文档](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## 后续步骤和其他资源

本指南介绍了如何在Experience Platform中管理审核日志。 有关如何监控平台活动的更多信息，请参阅 [可观测性洞察](../../../observability/home.md) 和 [监控数据摄取](../../../ingestion/quality/monitor-data-ingestion.md).

要加深您对Experience Platform中审核日志的了解，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
