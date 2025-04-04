---
title: 查看分析SQL
description: 查看您的配置文件、受众、目标和自定义见解背后的SQL，并通过查询编辑器按需执行查询。
exl-id: fd728926-c113-4593-92b1-916a02d09d41
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 查看分析SQL

使用[!UICONTROL 查看SQL]功能查看您的个人资料、受众、目标和自定义分析背后的SQL，并通过查询编辑器按需执行查询。 从SQL中获取40多种现有见解作为灵感，以创建新查询，这些查询可根据您的业务需求从Experience Platform数据获取独特的见解。

## 导航到功能板概述 {#navigate-to-overview}

要打开所选仪表板，请从左侧导航中选择&#x200B;**[!UICONTROL 用户档案]**、**[!UICONTROL 受众]**&#x200B;或&#x200B;**[!UICONTROL 目标]**。 如果工作区未自动显示，则接着从选项卡选项中选择&#x200B;**[!UICONTROL 概述]**。

或者，从左侧导航中选择&#x200B;**[!UICONTROL 功能板]**，后跟自定义功能板的名称。 此时将显示用户定义的仪表板的概述。

![突出显示具有[!UICONTROL 配置文件]、[!UICONTROL 受众]、[!UICONTROL 目标]和[!UICONTROL 仪表板]的Experience Platform UI。](./images/view-sql/dashboard-navigation.png)

## 查看SQL切换 {#toggle}

可以在配置文件、受众、目标和用户定义的功能板的概述中进行切换，以启用或禁用该功能。

>[!NOTE]
>
>如果启用了[!UICONTROL 查看SQL]切换，则在禁用该功能之前，无法更改全局和小组件级别的筛选器。

![高亮显示[!UICONTROL 查看SQL]切换。](./images/view-sql/view-sql-toggle.png)

启用此切换开关以在每个分析上显示[!UICONTROL 查看SQL]文本。

![突出显示了[!UICONTROL 查看SQL]的分析。](./images/view-sql/insight-view-sql.png)

选择&#x200B;**[!UICONTROL 查看SQL]**&#x200B;以打开包含构件的SQL的对话框。

## SQL对话框 {#sql-dialog}

此时将显示一个对话框，其中包含分析标题以及生成分析的SQL。

>[!TIP]
>
>通过选择复制图标（![复制图标），可以将整个SQL语句复制到剪贴板。](/help/images/icons/copy.png))。

![突出显示了SQL语句的洞察对话框。](./images/view-sql/sql-dialog.png)

选择&#x200B;**[!UICONTROL 运行SQL]**&#x200B;打开已预填充查询的查询编辑器。

![与[!UICONTROL 运行SQL]的洞察对话框突出显示。](./images/view-sql/run-sql.png)

## 编辑现有SQL {#edit-sql}

此时将显示“查询编辑器”。 您现在可以编辑报表，并以更符合您的报告需求的方式查询平台数据。 使用适当的名称保存您的新查询模板。

![已预填充包含您选择的分析SQL的查询编辑器。](./images/view-sql/edit-sql.png)

## 后续步骤

阅读本文档后，您现在了解如何在标准功能板或用户定义的功能板中访问SQL以获得任何见解。 如果您尚未这样做，则建议阅读[Real-Time Customer Data Platform分析数据模型文档](./data-models/cdp-insights-data-model-b2c.md)。 该文档包含有关根据您的营销和KPI需求为Real-Time CDP报表自定义SQL模板的见解。
