---
title: 查看分析SQL
description: 查看您的配置文件、受众、目标和自定义见解背后的SQL，并通过查询编辑器按需执行查询。
source-git-commit: be90cf38970a54431f48799bf506fb0a20ec0166
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 查看分析SQL

使用 [!UICONTROL 查看SQL] 功能以查看您的配置文件、受众、目标和自定义见解后面的SQL，并通过查询编辑器按需执行查询。 从SQL中获取40多种现有见解作为灵感，以创建新查询，这些查询可根据您的业务需求从Platform数据获取独特的见解。

## 导航到功能板概述 {#navigate-to-overview}

要打开所选仪表板，请选择 **[!UICONTROL 配置文件]**， **[!UICONTROL 受众]**，或 **[!UICONTROL 目标]** 从左侧导航栏中。 下次选择 **[!UICONTROL 概述]** 如果工作区未自动显示，则从选项卡选项中选中。

或者，选择 **[!UICONTROL 仪表板]** 左侧导航中，其后是自定义功能板的名称。 此时将显示用户定义的仪表板的概述。

![包含的Experience PlatformUI [!UICONTROL 配置文件]， [!UICONTROL 受众]， [!UICONTROL 目标]、和 [!UICONTROL 仪表板] 突出显示。](./images/view-sql/dashboard-navigation.png)

## 查看SQL切换 {#toggle}

可以在配置文件、受众、目标和用户定义的功能板的概述中进行切换，以启用或禁用该功能。

>[!NOTE]
>
>如果您启用 [!UICONTROL 查看SQL] 切换后，在禁用该功能之前，您将无法更改全局和小组件级别的筛选器。

![此 [!UICONTROL 查看SQL] 切换高亮显示。](./images/view-sql/view-sql-toggle.png)

启用切换以显示 [!UICONTROL 查看SQL] 每个单独洞察中的文本。

![见解 [!UICONTROL 查看SQL] 突出显示。](./images/view-sql/insight-view-sql.png)

选择 **[!UICONTROL 查看SQL]** 打开包含构件的SQL的对话框。

## SQL对话框 {#sql-dialog}

此时将显示一个对话框，其中包含分析标题以及生成分析的SQL。

>[!TIP]
>
>通过选择复制图标(![复制图标。](./images/view-sql/copy-icon.png))。

![突出显示带有SQL语句的洞察对话框。](./images/view-sql/sql-dialog.png)

选择 **[!UICONTROL 运行SQL]** 以打开查询编辑器，其中已预填充查询。

![与的洞察对话框 [!UICONTROL 运行SQL] 突出显示。](./images/view-sql/run-sql.png)

## 编辑现有SQL {#edit-sql}

此时将显示“查询编辑器”。 您现在可以编辑报表，并以更符合您的报告需求的方式查询平台数据。 使用适当的名称保存您的新查询模板。

![已预填充所选分析SQL的查询编辑器。](./images/view-sql/edit-sql.png)

## 后续步骤

阅读本文档后，您现在了解如何在标准功能板或用户定义的功能板中访问SQL以获得任何见解。 如果您尚未这样做，建议您阅读 [Real-time Customer Data Platform分析数据模型文档](./cdp-insights-data-model.md). 该文档包含有关根据您的营销和KPI需求为Real-Time CDP报表自定义SQL模板的见解。
