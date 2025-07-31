---
title: 创建全局过滤器
description: 了解如何使用自定义的全局应用过滤器过滤数据分析。
exl-id: a0084039-8809-4883-9f68-c666dcac5881
source-git-commit: 60b0c73766c89b98685810b4f58cfe1a40316dc9
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# 创建全局过滤器 {#create-global-filter}

若要创建全局筛选器，请首先从仪表板视图中选择&#x200B;**[!UICONTROL 添加筛选器]**，然后从下拉菜单中选择&#x200B;**[!UICONTROL 全局筛选器]**。

>[!IMPORTANT]
>
>确保将全局过滤器映射到所有图表。 这不是一个自动过程。 若要使用全局筛选器，必须在图表的SQL中包含[查询参数](../../../query-service/ui/parameterized-queries.md)，在构件编辑器中启用全局筛选器[，并在全局筛选器对话框中](#enable-global-filter)为参数选择运行时值[。 ](#select-global-filter)如果需要合并查询参数，请参阅query pro指南以了解如何编辑SQL。

![自定义仪表板的“添加筛选器”及其下拉菜单突出显示。](../../images/sql-insights-query-pro-mode/add-filter.png)

您可以使用自定义的全局筛选器快速更改SQL提供的洞察。

将打开[!UICONTROL 创建全局筛选器]对话框。 创建全局过滤器与使用SQL创建insight的过程相同。 首先，选择要查询的数据库（见解数据模型），然后在查询编辑器中输入自定义SQL，最后选择运行图标（![A运行图标。](/help/images/icons/play.png)）。

>[!IMPORTANT]
>
>在创建全局过滤器时，必须包含一个ID和一个值。 示例值允许您执行SQL语句并构建图表。 请注意，合成语句时提供的示例值会被您在运行时为日期或全局过滤器选择的实际值替换。

成功运行查询后，“结果”选项卡将显示结果。 选择&#x200B;**[!UICONTROL 下一步]**。

>[!NOTE]
>
>默认情况下，查询结果限制为100行。 要返回更多行，请使用所需的行数向SQL查询添加LIMIT子句。 要检索所有行并移除默认限制，请在查询中使用LIMIT 0。

![[!UICONTROL 创建全局筛选器对话框]包含数据集下拉菜单、运行图标和突出显示的下一步。](../../images/sql-insights-query-pro-mode/global-filter.png)

全局过滤器创建工作流的最后一步要求您为过滤器添加标签。 向&#x200B;**[!UICONTROL 筛选器标签]**&#x200B;文本字段添加标签，然后从下拉框中选择筛选器类型。

>[!NOTE]
>
>当前仅支持[!UICONTROL 组合框]筛选器类型选项。

最后，选择&#x200B;**[!UICONTROL 选择]**&#x200B;以返回到您的仪表板视图。

![[!UICONTROL 创建全局筛选器对话框]，其中的“选择”和“筛选器”标签文本输入突出显示。](../../images/sql-insights-query-pro-mode/global-filter-label.png)

## 为每个insight启用全局过滤器 {#enable-global-filter}

>[!TIP]
>
>在您创建的每个图表中启用全局过滤器。 这可确保您选择作为全局过滤器的值能够反映在所有图表中。

为功能板创建全局筛选器后，该全局筛选器的切换开关将作为小组件编辑器的一部分提供。

![带有全局筛选器切换的构件编辑器突出显示。](../../images/sql-insights-query-pro-mode/global-filter-consent.png)

>[!IMPORTANT]
>
>确保全局过滤器参数包含在每个insight的SQL中。

## 选择全局筛选器 {#select-global-filter}

要打开列出所有自定义筛选器的[!UICONTROL 筛选器]对话框，请选择筛选器图标（![筛选器图标）。](/help/images/icons/filter.png))。 接下来，要应用对您的仪表板分析的影响，请从全局筛选器的下拉菜单中选择一个选项，然后选择&#x200B;**[!UICONTROL 应用]**。

![突出显示筛选对话框的自定义仪表板。](../../images/sql-insights-query-pro-mode/custom-filters.png)

## 清除全局筛选器 {#clear-global-filter}

要清除所有自定义全局筛选器，请从&#x200B;**[!UICONTROL 筛选器]**&#x200B;对话框中选择[!UICONTROL 全部清除]。

![高亮显示带有“全部清除”的“筛选器”对话框。](../../images/sql-insights-query-pro-mode/clear-all.png)
