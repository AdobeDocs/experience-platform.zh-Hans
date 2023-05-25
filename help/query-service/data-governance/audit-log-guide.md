---
title: 查询服务审核日志集成
description: 查询服务审核日志维护各种用户操作的记录，形成审核跟踪，用于解决问题，或遵守公司数据管理政策和法规要求。 本教程概述了特定于查询服务的审核日志功能。
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] 审核日志集成

Adobe Experience Platform [!DNL Query Service] 审核日志集成提供与查询相关的用户操作记录。 审核日志是进行故障排除以及遵守公司数据管理政策和法规要求的重要工具。 利用功能，可返回多种事件类型的操作日志，并筛选和导出记录。 可以通过Platform UI或 [审核查询API](https://www.adobe.io/experience-platform-apis/references/audit-query/) 并以CSV或JSON文件格式下载。

要了解有关审核日志用户界面的更多信息，请参阅 [审核日志概述文档](../../landing/governance-privacy-security/audit-logs/overview.md). 要了解有关调用Platform API的更多信息，请参阅 [审核日志API指南](../../landing/api-guide.md).

## 先决条件

您必须拥有 [!DNL Data Governance] [!UICONTROL 查看用户活动日志] 启用了在Platform UI中查看审核日志仪表板的权限。 权限通过Adobe启用 [Admin Console](https://adminconsole.adobe.com/). 如果您没有启用此权限的管理员权限，请联系贵组织的管理员。 请参阅访问控制文档，了解 [有关通过Admin Console添加权限的完整说明](../../access-control/home.md).

## [!DNL Query Service] 审核日志类别 {#audit-log-categories}

审核日志类别提供者 [!DNL Query Service] 如下所示。

| 类别 | 描述 |
|---|---|
| [!UICONTROL 查询] | 此类别允许您审核查询执行。 |
| [!UICONTROL 查询模板] | 此类别允许您审核对查询模板执行的各种操作（创建、更新和删除）。 |
| [!UICONTROL 计划的查询] | 通过此类别，可审核在中创建、更新或删除的计划 [!DNL Query Service]. |

## 执行 [!DNL Query Service] 审核日志 {#perform-an-audit-log}

要执行审核，请执行以下操作 [!DNL Query Service] 活动，选择 **[!UICONTROL 审核]** 在左侧导航中，其后是漏斗图标(![过滤器图标。](../images/audit-log/filter.png))，以显示过滤器控件列表以帮助缩小结果范围。

![Platform UI审核日志仪表板，在左侧导航和筛选器控件中突出显示“审核”。](../images/audit-log/filter-controls.png)

从 [!UICONTROL 审核] 仪表板 [!UICONTROL 活动日志] 选项卡中，您可以通过任意一个 [!DNL Query Service] 类别。 可以根据日志结果执行的时间段、执行的操作/功能或执行查询的用户来进一步筛选日志结果。 请参阅审核日志文档，了解 [有关如何根据类别、操作、用户和状态筛选日志的完整说明](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

返回的审核日志数据包含以下关于满足所选筛选条件的所有查询的信息。

| 列名称 | 描述 |
|---|---|
| [!UICONTROL 时间戳] | 在中执行操作的确切日期和时间 `month/day/year hour:minute AM/PM` 格式。 |
| [!UICONTROL 资源名称] | 的值 [!UICONTROL 资源名称] 字段取决于选作过滤器的类别。 使用时 [!UICONTROL 计划的查询] 类别这是 **计划名称**. 使用时 [!UICONTROL 查询模板] 类别，这是 **模板名称**. 使用时 [!UICONTROL 查询] 类别，这是 **会话ID** |
| [!UICONTROL 类别] | 此字段与您从过滤器下拉列表中选择的类别匹配。 |
| [!UICONTROL 操作] | 这可以是创建、删除、更新或执行。 可用的操作取决于选作过滤器的类别。 |
| [!UICONTROL 用户] | 此字段提供执行查询的用户ID。 |

![突出显示筛选活动日志的审核仪表板。](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>通过下载CSV或JSON文件格式的日志结果，提供的查询详细信息将多于审计日志仪表板中默认显示的内容。

## 详细信息面板

选择审核日志结果的任意行，将在屏幕右侧打开一个详细信息面板。

![审核功能板“活动日志”选项卡，其中高亮显示详细信息面板。](../images/audit-log/details-panel.png)

详细信息面板可用于查找 [!UICONTROL 资产ID] 和 [!UICONTROL 事件状态].

的值 [!UICONTROL 资产ID] 更改情况取决于审核中使用的类别。

* 使用时 [!UICONTROL 查询] 类别， [!UICONTROL 资产ID] 是  **会话ID**.
* 使用时 [!UICONTROL 查询模板] 类别， [!UICONTROL 资产ID] 是 **模板Id** 并添加前缀 `[!UICONTROL templateID:]`.
* 使用时 [!UICONTROL 计划的查询] 类别， [!UICONTROL 资产ID] 是  **计划ID** 并添加前缀 `[!UICONTROL scheduleID:]`.

的值 [!UICONTROL 事件状态] 更改情况取决于审核中使用的类别。

* 使用时 [!UICONTROL 查询] 类别， [!UICONTROL 事件状态] 字段提供所有内容的列表 **查询Id** 由用户在该会话中执行。
* 使用时 [!UICONTROL 查询模板] 类别， [!UICONTROL 事件状态] 字段提供 **模板名称** 作为事件状态的前缀。
* 使用时 [!UICONTROL 查询计划] 类别， [!UICONTROL 事件状态] 字段提供 **计划名称** 作为事件状态的前缀。

## 可用的筛选条件 [!DNL Query Service] 审核日志类别 {#available-filters}

可用的过滤器因在下拉列表中选择的类别而异。 下表详细列出了可用于的过滤器 [[!DNL Query Service] 审核日志类别](#audit-log-categories).

| 过滤器 | 描述 |
|---|---|
| 类别 | 请参阅 [[!DNL Query Service] 审核日志类别](#audit-log-categories) 部分，以获取可用类别的完整列表。 |
| 操作 | 当引用时 [!DNL Query Service] 审计类别，更新为 **对现有表单的修改**，删除是 **删除时间表或模板**，创建是 **创建新计划或模板**，并且执行为 **运行查询**. |
| 用户 | 输入完整的用户ID(例如，johndoe@acme.com)以按用户进行筛选。 |
| 状态 | 此 [!UICONTROL 允许]， [!UICONTROL 成功]、和 [!UICONTROL 失败] 选项根据“状态”或“事件状态”筛选日志，而 [!UICONTROL 拒绝] 选项将被过滤掉 **所有** 日志。 |
| 日期 | 选择开始日期和/或结束日期，以定义筛选结果的日期范围。 |

## 后续步骤

通过阅读本文档，您对 [!DNL Query Service] 审核日志功能以及如何使用该功能筛选 [!DNL Query Service] 用户操作。

如果您使用 [!DNL Query Service] 审核日志功能出于疑难解答目的，建议您阅读 [疑难解答指南](../troubleshooting-guide.md).
