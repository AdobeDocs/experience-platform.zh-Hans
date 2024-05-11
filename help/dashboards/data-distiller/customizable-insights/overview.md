---
title: 扩展应用程序报表的可自定义分析
description: 了解如何使用SQL查询生成自定义仪表板的见解。
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 扩展应用程序报表的可自定义分析

使用自定义SQL查询从各种结构化数据集有效提取洞察。 技术人员可以使用查询专业模式执行复杂的SQL分析，然后通过自定义仪表板上的图表与非技术用户共享此分析或将它们导出为CSV文件。 这种洞察创建方法非常适合具有明确关系的表，并且允许在洞察和过滤器中进行更大程度的自定义，以适应小范围用例。

>[!IMPORTANT]
>
>Query Pro模式仅适用于已购买 [数据Distiller SKU](../../../query-service/data-distiller/overview.md).

要从SQL生成见解，必须首先创建功能板。

## 创建自定义仪表板 {#create-custom-dashboard}

要创建自定义仪表板，请选择 **[!UICONTROL 仪表板]** 从左侧导航面板中打开功能板工作区。 接下来，选择 **[!UICONTROL 创建功能板]**.

![突出显示包含“创建”功能板的功能板库存。](../../images/customizable-insights/create-dashboard.png)

此 **[!UICONTROL 创建功能板]** 出现对话框。 有两个选项可供您选择功能板创建方法。 要创建见解，您可以使用现有数据模型与 [[!UICONTROL 引导式设计模式]](../../user-defined-dashboards.md) 或您自己的SQL [!UICONTROL Query pro模式].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

使用现有数据模型的优点在于，它可以为您的特定业务需求提供结构化、高效和可伸缩的框架。 学习如何 [从现有数据模型创建见解](../../user-defined-dashboards.md#create-widget)，请参阅自定义功能板指南。

从SQL查询生成的见解提供了更大的灵活性和自定义设置。 技术人员可以使用查询专业模式对SQL执行复杂的分析，然后通过此仪表板功能与非技术用户共享此分析。 选择 **[!UICONTROL Query pro模式]** 后接 **[!UICONTROL 保存]**.

>[!NOTE]
>
>做出选择后，将无法在该功能板中更改此选择。 相反，您必须使用不同的仪表板创建方法创建新仪表板。

![此 [!UICONTROL 创建功能板] 对话框，其中的“Query pro”模式和“Save”突出显示。](../../images/customizable-insights/query-pro-mode.png)

## 创建图表 {#create-a-chart}

请参阅 [query pro mode指南](./query-pro-mode.md) 有关使用SQL创建图表的分步说明。
