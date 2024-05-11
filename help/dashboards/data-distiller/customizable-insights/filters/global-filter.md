---
title: 创建全局过滤器
description: 了解如何使用自定义的全局应用过滤器过滤数据分析。
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 创建全局过滤器 {#create-global-filter}

要创建全局过滤器，请先选择 **[!UICONTROL 添加筛选器]** 从仪表板视图中，然后 **[!UICONTROL 全局筛选器]** 下拉菜单中。

>[!IMPORTANT]
>
>确保将全局过滤器映射到所有图表。 这不是一个自动过程。 要使用全局过滤器，您必须包含 [查询参数](../../../../query-service/ui/parameterized-queries.md) 在图表的SQL中， [启用全局过滤器](#enable-global-filter) 在小组件编辑器中，和 [选择运行时值](#select-global-filter) 全局筛选器对话框中的参数。 如果需要合并查询参数，请参阅query pro指南以了解如何编辑SQL。

![一个自定义仪表板，其中添加过滤器及其下拉菜单突出显示。](../../../images/customizable-insights/add-filter.png)

您可以使用自定义的全局筛选器快速更改SQL提供的洞察。

此 [!UICONTROL 创建全局过滤器] 对话框打开。 创建全局过滤器与使用SQL创建洞察的过程相同。 首先，选择要查询的数据库（见解数据模型），然后在查询编辑器中输入自定义SQL，最后选择运行图标(![运行图标。](../../../images/customizable-insights/run-icon.png))。

>[!IMPORTANT]
>
>在创建全局过滤器时，必须包含一个ID和一个值。 示例值允许您执行SQL语句并构建图表。 请注意，合成语句时提供的示例值会被您在运行时为日期或全局过滤器选择的实际值替换。

成功运行查询后，“结果”选项卡将显示结果。 选择&#x200B;**[!UICONTROL 下一步]**。

![此 [!UICONTROL 创建全局过滤器对话框] 使用数据集下拉菜单，运行图标和下一步会突出显示。](../../../images/customizable-insights/global-filter.png)

全局过滤器创建工作流的最后一步要求您为过滤器添加标签。 将标签添加到 **[!UICONTROL 筛选标签]** 文本字段，并从下拉框中选择过滤器类型。

>[!NOTE]
>
>仅 [!UICONTROL 组合框] 当前支持筛选器类型选项。

最后，选择 **[!UICONTROL 选择]** 以返回到仪表板视图。

![此 [!UICONTROL 创建全局过滤器对话框] 选择，并突出显示过滤器标签文本输入。](../../../images/customizable-insights/global-filter-label.png)

## 为每个分析启用全局过滤器 {#enable-global-filter}

>[!TIP]
>
>在您创建的每个图表中启用全局过滤器。 这可确保您选择作为全局过滤器的值能够反映在所有图表中。

为功能板创建全局筛选器后，该全局筛选器的切换开关将作为小组件编辑器的一部分提供。

![突出显示具有“全局过滤器”切换的小组件编辑器。](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>确保每个分析的SQL中都包含全局过滤器参数。

## 选择全局筛选器 {#select-global-filter}

打开 [!UICONTROL 过滤器] 列出所有自定义筛选器的对话框，请选择筛选器图标(![过滤器图标。](../../../images/customizable-insights/filter.png))。 接下来，要应用对功能板分析的影响，请从全局筛选器的下拉菜单中选择一个选项，然后选择 **[!UICONTROL 应用]**.

![突出显示过滤器对话框的自定义仪表板。](../../../images/customizable-insights/custom-filters.png)
