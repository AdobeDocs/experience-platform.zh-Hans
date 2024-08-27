---
title: 用于扩展应用程序报表的SQL分析
description: 了解如何使用SQL查询生成自定义仪表板的见解。
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 3435ddd4b235c1c66cd29c75b779bcca607a5d4f
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 用于扩展应用程序报表的SQL分析

使用自定义SQL查询从各种结构化数据集有效提取洞察。 技术人员可以使用查询专业模式执行复杂的SQL分析，然后通过自定义仪表板上的图表与非技术用户共享此分析或将它们导出为CSV文件。 这种洞察创建方法非常适合具有明确关系的表，并且允许在洞察和过滤器中进行更大程度的自定义，以适应小范围用例。

>[!IMPORTANT]
>
>查询专业模式仅适用于已购买[Data Distiller SKU](../../../query-service/data-distiller/overview.md)的用户。

要从SQL生成见解，必须首先创建功能板。

## 创建自定义仪表板 {#create-custom-dashboard}

要创建自定义仪表板，请从左侧导航面板中选择&#x200B;**[!UICONTROL 仪表板]**&#x200B;以打开仪表板工作区。 接下来，选择&#x200B;**[!UICONTROL 创建仪表板]**。

![突出显示了“创建仪表板”的功能板库存。](../../images/sql-insights/create-dashboard.png)

出现&#x200B;**[!UICONTROL 创建仪表板]**&#x200B;对话框。 有两个选项可供您选择功能板创建方法。 若要创建您的见解，您可以使用具有[[!UICONTROL 引导式设计模式]](../../user-defined-dashboards.md)的现有数据模型，或者使用[!UICONTROL Query pro模式]的您自己的SQL。

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

使用现有数据模型的优点在于，它可以为您的特定业务需求提供结构化、高效和可伸缩的框架。 要了解如何[从现有数据模型](../../user-defined-dashboards.md#create-widget)创建见解，请参阅自定义仪表板指南。

从SQL查询生成的见解提供了更大的灵活性和自定义设置。 技术人员可以使用查询专业模式对SQL执行复杂的分析，然后通过此仪表板功能与非技术用户共享此分析。 选择&#x200B;**[!UICONTROL Query pro模式]**，然后选择&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>做出选择后，将无法在该功能板中更改此选择。 相反，您必须使用不同的仪表板创建方法创建新仪表板。

![高亮显示了[!UICONTROL 创建仪表板]对话框，其中显示了Query pro模式和“保存”。](../../images/sql-insights/query-pro-mode.png)

## 创建图表 {#create-a-chart}

有关使用SQL创建图表的分步说明，请参阅[查询专业模式指南](../query-pro-mode/overview.md)。
