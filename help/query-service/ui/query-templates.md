---
title: 查询模板
description: 查询模板是可重用的已保存SQL查询，其他用户可重复使用它们以节省时间和精力。 它们可以使用查询编辑器或查询服务API创建，并可用于所有Experience Platform数据集。
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: 1a44be939a4678078b414658199472e07dee153b
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# 查询模板

Adobe Experience Platform查询服务允许您以查询模板的形式保存和重用SQL代码。 模板可避免重复执行常见任务，从而节省精力。 您可以在组织内共享模板并轻松地更改查询值，而无需访问或了解底层SQL。

本文档提供了在查询服务中创建查询模板所需的信息。

## 先决条件

您必须拥有 [!UICONTROL 管理查询] 启用了以下权限：访问查询编辑器并在Platform UI中查看查询仪表板。 权限通过Adobe启用 [Admin Console](https://adminconsole.adobe.com/). 如果您没有启用此权限的管理员权限，请联系贵组织的管理员。 请参阅访问控制文档，了解 [有关通过Admin Console添加权限的完整说明](../../access-control/home.md).

## 创建查询模板

您可以通过两种方法创建查询模板，即向查询服务API发出POST请求 `query-templates` 终结点，或者通过查询编辑器编写、命名和保存查询。

### 使用查询编辑器创作查询并将其另存为模板

有关如何使用查询编辑器执行以下操作的说明，请参阅文档 [写入](./user-guide.md#query-authoring) 和 [保存查询](./user-guide.md#saving-queries). 命名并保存查询后，便可将查询作为查询模板重复使用。 [!UICONTROL 模板] 选项卡。

>[!TIP]
>
>在查询编辑器中保存查询时，将会弹出一条确认消息，通知您操作成功。 此弹出消息包含一个链接，为导航到查询计划工作区提供了一种便捷的方法。 请参阅 [计划查询文档](./query-schedules.md) 以了解如何以自定义节奏运行查询。

## 浏览查询模板 {#browse}

从Platform UI的查询工作区中，选择 **[!UICONTROL 模板]** 显示可用已保存查询的列表。

![突出显示“模板”选项卡的查询工作区。](../images/ui/query-templates/query-templates.png)

要查找相关的模板信息，请从可用列表中选择任意查询模板以打开详细信息面板。

![查询工作区中查询ID突出显示的详细信息面板。](../images/ui/query-templates/details-panel.png)

从详细信息面板中，您可以执行以下操作：

* 选择 **[!UICONTROL 作为CTA运行]** 通过从一个或多个现有表中选择数据来创建新表。 此选项仅在您有SELECT查询时才可用。
* 选择 **[!UICONTROL 添加计划]** 以开始编辑查询模板的计划。
* 选择 **[!UICONTROL 查看计划]** 导航到 [!UICONTROL 时间表] 查询编辑器的选项卡。 此视图包含与查询关联的任何计划信息。
* 选择 **[!UICONTROL 删除查询]** 以删除模板。
* 选择模板名称以导航到查询编辑器，在该编辑器中预填充了SQL以供编辑。

### 使用查询服务API创建模板

有关说明，请参阅文档 [如何创建查询模板](../api/query-templates.md#create-a-query-template) 使用查询服务API。 新创建的查询模板的详细信息包含在响应正文中。

>[!NOTE]
>
>使用API创建的模板也显示在Platform UI查询服务模板选项卡中。

## 后续步骤

通过阅读本文档，您现在可以更好地了解如何在查询服务中创建查询模板。 请参阅 [UI概述](./overview.md)，或 [查询服务API指南](../api/getting-started.md) 了解有关查询服务功能的更多信息。

请参阅 [计划查询端点指南](../api/scheduled-queries.md) 了解如何使用API计划查询，或者 [查询编辑器指南](./user-guide.md#scheduled-queries) 用于UI。
