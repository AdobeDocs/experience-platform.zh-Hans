---
title: 查询服务审核日志集成
description: 查询服务审核日志维护各种用户操作的记录，以形成用于解决问题或遵守公司数据管理策略和法规要求的审核跟踪。 本教程概述了特定于查询服务的审核日志功能。
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: 12b717be67cb35928d84e83b6d692f9944d651d8
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# [!DNL Query Service] 审核日志集成

Adobe Experience Platform [!DNL Query Service] 审核日志集成提供与查询相关的用户操作记录。 审核日志是疑难解答和遵守公司数据管理策略和法规要求的必不可少的工具。 利用功能，可返回许多事件类型的操作日志，并过滤和导出记录。 日志可通过Platform UI访问，或 [审核查询API](https://www.adobe.io/experience-platform-apis/references/audit-query/) ，并以CSV或JSON文件格式下载。

要了解有关审核日志用户界面的更多信息，请参阅 [审核日志概述文档](../../landing/governance-privacy-security/audit-logs/overview.md). 要了解有关调用Platform API的更多信息，请参阅 [审核日志API指南](../../landing/api-guide.md).

## 先决条件

您必须拥有 [!DNL Data Governance] [!UICONTROL 查看用户活动日志] 在Platform UI中启用了查看审核日志功能板的权限。 权限通过Adobe启用 [Admin Console](https://adminconsole.adobe.com/). 如果您没有启用此权限的管理员权限，请联系贵组织的管理员。 请参阅的访问控制文档 [有关通过Admin Console添加权限的完整说明](../../access-control/home.md).

## [!DNL Query Service] 审核日志类别 {#audit-log-categories}

提供的审核日志类别 [!DNL Query Service] 如下所示。

| 类别 | 描述 |
|---|---|
| [!UICONTROL 计划查询] | 利用此类别，可审核在 [!DNL Query Service]. |
| [!UICONTROL 查询模板] | 利用此类别，可审核对查询模板执行的各种操作（创建、更新和删除）。 |
<!-- | [!UICONTROL Query] | This category allows you to audit query executions. | -->

## 执行 [!DNL Query Service] 审核日志 {#perform-an-audit-log}

执行审核 [!DNL Query Service] 活动，选择 **[!UICONTROL 审核]** 从左侧导航中，接下漏斗图标(![过滤器图标。](../images/audit-log/filter.png))以显示筛选器控件列表，以帮助缩小结果范围。

![Platform UI审核日志功能板左侧导航中带有“审核”，过滤器控件突出显示。](../images/audit-log/filter-controls.png)

从 [!UICONTROL 审核] 仪表板 [!UICONTROL 活动日志] 选项卡上，您可以按 [!DNL Query Service] 类别。 可以根据执行日志结果的时间段、执行的操作/函数或颁布查询的用户，进一步过滤日志结果。 请参阅的审核日志文档 [有关如何根据类别、操作、用户和状态过滤日志的完整说明](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

返回的审核日志数据包含有关满足您选择的筛选条件的所有查询的以下信息。

| 列名称 | 描述 |
|---|---|
| [!UICONTROL 时间戳] | 在 `month/day/year hour:minute AM/PM` 格式。 |
| [!UICONTROL 资产名称] | 的值 [!UICONTROL 资产名称] 字段取决于选择作为过滤器的类别。 使用 [!UICONTROL 计划查询] 类别，这是 **计划名称**. 使用 [!UICONTROL 查询模板] 类别，这是 **模板名称**. |
| [!UICONTROL 类别] | 此字段与您在过滤器下拉菜单中选择的类别匹配。 |
| [!UICONTROL 操作] | 这可以是创建、删除、更新或执行。 可用的操作取决于选择作为过滤器的类别。 |
| [!UICONTROL 用户] | 此字段提供执行查询的用户ID。 |

![“审核”功能板中突出显示了过滤的活动日志。](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>与审核日志功能板中默认显示的相比，通过下载CSV或JSON文件格式的日志结果来提供更多查询详细信息。

选择任意行的审核日志结果，以打开屏幕右侧的详细信息面板。

![审核功能板活动日志选项卡，其中突出显示了详细信息面板。](../images/audit-log/details-panel.png)

>[!NOTE]
>
>详细信息面板可用于查找 [!UICONTROL 资产ID]. 的值 [!UICONTROL 资产ID] 更改取决于审核中使用的类别。 使用 [!UICONTROL 查询模板] 类别， [!UICONTROL 资产ID] 是 **模板ID**. 使用 [!UICONTROL 计划查询] 类别， [!UICONTROL 资产ID] 是  **计划ID**.

## 可用的过滤器 [!DNL Query Service] 审核日志类别 {#available-filters}

可用的过滤器因下拉列表中选择的类别而异。 下表详细列出了 [[!DNL Query Service] 审核日志类别](#audit-log-categories).

| 过滤器 | 描述 |
|---|---|
| 类别 | 请参阅 [[!DNL Query Service] 审核日志类别](#audit-log-categories) 部分。 |
| 操作 | 在 [!DNL Query Service] 审核类别，更新是 **对现有表单的修改**，删除是 **删除计划或模板**，创建为 **创建新计划或模板**，和执行正在运行查询。 |
| 用户 | 输入完整的用户ID(例如johndoe@acme.com)以按用户进行过滤。 |
| 状态 | 此过滤器不适用于 [!DNL Query Service] 审核日志。 的 [!UICONTROL 允许], [!UICONTROL 成功]和 [!UICONTROL 失败] 选项将不会筛选结果，而 [!UICONTROL 拒绝] 选项将筛选 **全部** 日志。 |
| 日期 | 选择开始日期和/或结束日期，以定义日期范围以按过滤结果。 |

## 后续步骤

通过阅读本文档，您对 [!DNL Query Service] 审核日志功能以及如何使用它过滤您的 [!DNL Query Service] 用户操作。

如果您使用 [!DNL Query Service] 出于疑难解答目的，建议您阅读 [疑难解答指南](../troubleshooting-guide.md).
