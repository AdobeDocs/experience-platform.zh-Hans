---
title: 查询服务审核日志集成
description: 查询服务审核日志维护各种用户操作的记录，形成审核跟踪，用于解决问题，或遵守公司数据管理政策和法规要求。 本教程概述了特定于查询服务的审核日志功能。
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 1%

---

# [!DNL Query Service]审核日志集成

Adobe Experience Platform [!DNL Query Service]审核日志集成提供查询相关用户操作的记录。 审核日志是进行故障排除并遵守公司数据管理政策和法规要求的重要工具。 利用功能，可返回多种事件类型的操作日志，并过滤和导出记录。 可以通过Experience Platform UI或[审核查询API](https://www.adobe.io/experience-platform-apis/references/audit-query/)访问日志，并以CSV或JSON文件格式下载。

要了解有关审核日志用户界面的详细信息，请参阅[审核日志概述文档](../../landing/governance-privacy-security/audit-logs/overview.md)。 要了解有关调用Experience Platform API的更多信息，请参阅[审核日志API指南](../../landing/api-guide.md)。

## 先决条件

您必须启用[!DNL Data Governance] [!UICONTROL 查看用户活动日志]权限才能在Experience Platform UI中查看审核日志仪表板。 该权限是通过Adobe [Admin Console](https://adminconsole.adobe.com/)启用的。 如果您没有启用此权限的管理员权限，请联系贵组织的管理员。 有关通过Admin Console[&#128279;](../../access-control/home.md)添加权限的完整说明，请参阅访问控制文档。

## [!DNL Query Service]审核日志类别 {#audit-log-categories}

[!DNL Query Service]提供的审核日志类别如下。

| 类别 | 描述 |
|---|---|
| [!UICONTROL 查询] | 此类别允许您审核查询执行。 |
| [!UICONTROL 查询模板] | 此类别允许您审核对查询模板执行的各种操作（创建、更新和删除）。 |
| [!UICONTROL 计划的查询] | 此类别允许您审核在[!DNL Query Service]内创建、更新或删除的计划。 |

## 执行[!DNL Query Service]审核日志 {#perform-an-audit-log}

要对[!DNL Query Service]活动执行审核，请从左侧导航中选择&#x200B;**[!UICONTROL 审核]**，然后选择漏斗图标（![过滤器图标）。](/help/images/icons/filter.png))以显示筛选器控件列表以帮助缩小结果范围。

![Experience Platform UI审核日志仪表板在左侧导航和筛选器控件中突出显示“审核”。](../images/audit-log/filter-controls.png)

从[!UICONTROL 审核]仪表板[!UICONTROL 活动日志]选项卡中，您可以按[!DNL Query Service]类别中的任意类别筛选所有记录的Experience Platform操作。 可以根据日志结果执行的时段、执行的操作/功能或执行查询的用户来进一步筛选日志结果。 有关如何根据类别、操作、用户和状态筛选日志的完整说明[，请参阅审核日志文档](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui)。

返回的审核日志数据包含以下关于满足所选筛选条件的所有查询的信息。

| 列名 | 描述 |
|---|---|
| [!UICONTROL 时间戳] | 以`month/day/year hour:minute AM/PM`格式执行的操作的确切日期和时间。 |
| [!UICONTROL 资源名称] | [!UICONTROL 资源名称]字段的值取决于选择作为筛选器的类别。 使用[!UICONTROL 计划查询]类别时，这是&#x200B;**计划名称**。 使用[!UICONTROL 查询模板]类别时，这是&#x200B;**模板名称**。 使用[!UICONTROL 查询]类别时，这是&#x200B;**会话ID** |
| [!UICONTROL 类别] | 此字段与您在“筛选器”下拉列表中选择的类别匹配。 |
| [!UICONTROL 操作] | 这可以是创建、删除、更新或执行。 可用的操作取决于选作过滤器的类别。 |
| [!UICONTROL 用户] | 此字段提供执行查询的用户ID。 |

![已突出显示筛选活动日志的审核仪表板。](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>通过以CSV或JSON文件格式下载日志结果，提供的查询详细信息比审计日志仪表板中默认显示的多。

## 详细信息面板

选择审核日志结果的任意行，将在屏幕右侧打开一个详细信息面板。

![审核突出显示详细信息面板的仪表板“活动日志”选项卡。](../images/audit-log/details-panel.png)

详细信息面板可用于查找[!UICONTROL 资产ID]和[!UICONTROL 事件状态]。

[!UICONTROL 资产ID]的值会因审核中使用的类别而异。

* 使用[!UICONTROL 查询]类别时，[!UICONTROL 资产ID]是&#x200B;**会话ID**。
* 使用[!UICONTROL 查询模板]类别时，[!UICONTROL 资产ID]是&#x200B;**模板ID**，前缀为`[!UICONTROL templateID:]`。
* 使用[!UICONTROL 计划查询]类别时，[!UICONTROL 资产ID]是&#x200B;**计划ID**，前缀为`[!UICONTROL scheduleID:]`。

[!UICONTROL 事件状态]的值会根据审核中使用的类别进行更改。

* 使用[!UICONTROL 查询]类别时，[!UICONTROL 事件状态]字段提供了用户在该会话中执行的所有&#x200B;**查询ID**&#x200B;的列表。
* 使用[!UICONTROL 查询模板]类别时，[!UICONTROL 事件状态]字段提供&#x200B;**模板名称**&#x200B;作为事件状态的前缀。
* 使用[!UICONTROL 查询计划]类别时，[!UICONTROL 事件状态]字段提供&#x200B;**计划名称**&#x200B;作为事件状态的前缀。

## [!DNL Query Service]审核日志类别的可用筛选器 {#available-filters}

可用的过滤器因在下拉列表中选择的类别而异。 下表详细列出了[[!DNL Query Service] 审核日志类别](#audit-log-categories)可用的筛选器。

| 筛选条件 | 描述 |
|---|---|
| 类别 | 有关可用类别的完整列表，请参阅[[!DNL Query Service] 审核日志类别](#audit-log-categories)部分。 |
| 操作 | 在引用[!DNL Query Service]审核类别时，更新是对现有表单的&#x200B;**修改**，删除是对计划或模板的&#x200B;**删除**，创建是&#x200B;**创建新计划或模板**，执行是&#x200B;**运行查询**。 |
| 用户 | 输入完整的用户ID(例如，johndoe@acme.com)以按用户进行筛选。 |
| 状态 | [!UICONTROL 允许]、[!UICONTROL 成功]和[!UICONTROL 失败]选项将根据“状态”或“事件状态”筛选日志，而[!UICONTROL 拒绝]选项将筛选&#x200B;**所有**&#x200B;日志。 |
| 日期 | 选择开始日期和/或结束日期，以定义筛选结果的日期范围。 |

## 后续步骤

通过阅读本文档，您可以更好地了解[!DNL Query Service]审核日志功能，以及如何使用它来筛选您的[!DNL Query Service]用户操作。

如果您使用[!DNL Query Service]审核日志功能进行疑难解答，建议您阅读[疑难解答指南](../troubleshooting-guide.md)。
