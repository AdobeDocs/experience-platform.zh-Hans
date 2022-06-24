---
title: 查询模板
description: 查询模板是可重用的已保存SQL查询，其他用户可重复使用这些查询以节省时间和精力。 它们可以使用查询编辑器或查询服务API创建，并可用于所有Experience Platform数据集。
source-git-commit: 5ed822ec16e8e8d38e93370440242ec4c1c01320
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# 查询模板

Adobe Experience Platform查询服务允许您以查询模板的形式保存和重用SQL代码。 模板可避免重复通常执行的任务，从而节省了工作量。 您可以在组织内共享模板，并轻松更改查询值，而无需访问或了解基础SQL。

本文档提供了在查询服务中创建查询模板所需的信息。

## 先决条件

您必须拥有 [!UICONTROL 管理查询] 启用了访问查询编辑器和在Platform UI中查看查询功能板的权限。 权限通过Adobe启用 [Admin Console](https://adminconsole.adobe.com/). 如果您没有启用此权限的管理员权限，请联系贵组织的管理员。 请参阅的访问控制文档 [有关通过Admin Console添加权限的完整说明](../../access-control/home.md).

## 创建查询模板

您可以通过两种方法创建查询模板，方法是向查询服务API发出POST请求 `query-templates` 端点，或通过编写、命名和通过查询编辑器保存查询来实现此目的。

### 使用查询编辑器创作查询并将其另存为模板

有关如何使用查询编辑器以 [写入](./user-guide.md#query-authoring) 和 [保存查询](./user-guide.md#saving-queries). 命名并保存查询后，该查询便可在 [!UICONTROL 浏览] 选项卡。

从Platform UI的“查询”工作区中，选择 **[!UICONTROL 浏览]** 以显示可用的已保存查询列表。

![查询工作区中突出显示了“浏览”选项卡。](../images/ui/query-templates/query-templates.png)

要查找相关的模板信息，请从可用列表中选择任意查询模板以打开详细信息面板。

![查询工作区中的详细信息面板，其中突出显示了查询ID。](../images/ui/query-templates/details-panel.png)

### 使用查询服务API创建模板

有关 [如何创建查询模板](../api/query-templates.md#create-a-query-template) 使用查询服务API。 新创建的查询模板的详细信息包含在响应正文中。

>[!NOTE]
>
>使用API创建的模板也会显示在Platform UI查询服务浏览选项卡中。

## 后续步骤

通过阅读本文档，您现在可以更好地了解如何在查询服务中创建查询模板。 请参阅 [UI概述](./overview.md)，或 [查询服务API指南](../api/getting-started.md) 以了解有关查询服务功能的更多信息。

请参阅 [计划查询终结点指南](../api/scheduled-queries.md) 了解如何使用API计划查询，或 [查询编辑器指南](./user-guide.md#scheduled-queries) （在UI中）。
